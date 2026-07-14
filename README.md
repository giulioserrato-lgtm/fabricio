# Ponto do Fabrício — guia de configuração

Este site mostra o ponto (entrada/saída) do Fabrício de segunda a sexta, no mês atual, e salva tudo num banco de dados compartilhado (Firebase), para que você e suas irmãs vejam sempre os mesmos registros, de qualquer celular ou computador.

Arquivos deste pacote:
- `index.html` → a página em si
- `manifest.json` → permite instalar a página como app no Android
- `icone-192.png`, `icone-512.png`, `icone-apple-180.png` → ícones do app
- `firestore.rules` → regra de segurança para colar no Firebase (não vai para o site)
- `README.md` → este guia

Envie **todos os arquivos acima, exceto o `firestore.rules` e o `README.md`**, para o mesmo repositório do GitHub, na mesma pasta (não precisa criar subpastas).

## Parte 1 — Criar o banco de dados no Firebase (gratuito)

1. Acesse **console.firebase.google.com** e faça login com uma conta Google.
2. Clique em **Adicionar projeto**, dê um nome (ex: `ponto-fabricio`) e siga os passos (pode desativar o Google Analytics, não é necessário).
3. Dentro do projeto, no menu lateral, clique em **Compilação → Firestore Database**.
4. Clique em **Criar banco de dados**.
   - Escolha o modo **Produção**.
   - Escolha uma localização (ex: `southamerica-east1` para servidores no Brasil).
5. Depois de criado, vá na aba **Regras** dentro do Firestore e substitua o conteúdo pelo texto do arquivo `firestore.rules` que te entreguei. Clique em **Publicar**.
6. Agora volte para a **Visão geral do projeto** (ícone de engrenagem → Configurações do projeto).
7. Em **Seus aplicativos**, clique no ícone **</>** (Web) para criar um app da Web.
   - Dê um apelido (ex: `ponto-web`) e clique em **Registrar app**.
   - Não precisa marcar "Firebase Hosting".
8. O Firebase vai te mostrar um bloco de código parecido com este:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "ponto-fabricio.firebaseapp.com",
  projectId: "ponto-fabricio",
  storageBucket: "ponto-fabricio.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

9. Copie esses 6 valores.

## Parte 2 — Colar a configuração no arquivo `index.html`

1. Abra o arquivo `index.html` em qualquer editor de texto (pode ser o Bloco de Notas, o próprio GitHub, ou o VS Code).
2. Procure este trecho perto do final do arquivo (dentro de `<script type="module">`):

```js
const firebaseConfig = {
  apiKey: "SUA_API_KEY_AQUI",
  authDomain: "SEU_PROJETO.firebaseapp.com",
  projectId: "SEU_PROJETO",
  storageBucket: "SEU_PROJETO.appspot.com",
  messagingSenderId: "SEU_SENDER_ID",
  appId: "SEU_APP_ID"
};
```

3. Substitua os 6 valores pelos que você copiou do Firebase no passo anterior. Salve o arquivo.

> Enquanto esses valores não forem preenchidos, a página mostra o aviso "Firebase ainda não configurado" no topo.

## Parte 3 — Subir para o GitHub

1. Crie uma conta em **github.com**, se ainda não tiver.
2. Clique em **New repository**, dê um nome (ex: `ponto-fabricio`), deixe **Public** e clique em **Create repository**.
3. Na tela do repositório, clique em **Add file → Upload files**.
4. Arraste **todos estes arquivos juntos**: `index.html`, `manifest.json`, `icone-192.png`, `icone-512.png` e `icone-apple-180.png`.
5. Clique em **Commit changes**.

## Parte 4 — Publicar no Netlify

1. Acesse **app.netlify.com** e faça login (pode usar a conta do GitHub).
2. Clique em **Add new site → Import an existing project**.
3. Escolha **GitHub** e selecione o repositório `ponto-fabricio`.
4. Não precisa preencher comando de build nem pasta de publicação — deixe em branco e clique em **Deploy site**.
5. Em alguns segundos, o Netlify gera um link (algo como `https://ponto-fabricio-123.netlify.app`). Esse é o link que você compartilha com suas irmãs.

## Como funciona no dia a dia

- No topo da página há um seletor de mês (com setas ‹ › e uma lista) que vai de **janeiro de 2026 até o mês atual**. Conforme os meses forem passando, o mês novo aparece automaticamente nessa lista — não precisa fazer nada.
- Ao abrir a página, ela já mostra o **mês atual** selecionado, com o dia de hoje destacado e a tela rolando até ele.
- Todo dia útil sem horário marcado já vem preenchido com **09:00 de entrada e 19:00 de saída** — é só editar quando o horário real for diferente.
- Sempre que alguém preencher entrada, saída ou marcar falta, isso é salvo na nuvem na hora, para o mês selecionado.
- Se duas pessoas abrirem o link ao mesmo tempo, ambas veem as mesmas informações atualizadas automaticamente, sem precisar atualizar a página.
- O botão **Limpar mês selecionado** apaga os registros do mês que está sendo exibido no momento — agora exige um **código de confirmação** antes de apagar. O código padrão no arquivo é `1234`; procure por `CODIGO_PARA_LIMPAR` dentro do `index.html` e troque por um código só seu antes de publicar o site. Importante: essa é uma proteção simples (funciona bem para evitar cliques por engano ou curiosidade), mas não é uma segurança à prova de blindagem — alguém com conhecimento técnico ainda poderia contornar. Para uma proteção mais forte, seria necessário adicionar login (Firebase Authentication).
- No canto superior direito há os botões **A− / A+** para diminuir ou aumentar o tamanho do texto da página inteira, útil para quem tem dificuldade de leitura; a preferência fica salva no navegador de cada pessoa.

## Parte 5 — Instalar como app no celular

Depois que o link do Netlify estiver no ar, cada pessoa faz esse passo **uma vez, no próprio celular**:

### No Android (Google Chrome)
1. Abra o link do site no Chrome.
2. Toque nos **três pontinhos** (⋮) no canto superior direito.
3. Toque em **Adicionar à tela inicial** (ou **Instalar app**, dependendo da versão do Chrome).
4. Confirme o nome "Ponto Fabrício" e toque em **Adicionar**.
5. Um ícone azul com a letra "F" aparece na tela inicial, e abre em tela cheia, como um app de verdade.

### No iPhone (Safari)
1. Abra o link do site no **Safari** (precisa ser o Safari, não funciona pelo Chrome no iPhone).
2. Toque no ícone de **compartilhar** (o quadrado com uma seta para cima), na barra inferior.
3. Role para baixo e toque em **Adicionar à Tela de Início**.
4. Confirme o nome e toque em **Adicionar**, no canto superior direito.
5. O ícone aparece na tela inicial, e abre sem as barras do navegador, como um app.

Isso não precisa ser feito de novo — uma vez instalado, o ícone continua funcionando, buscando sempre os dados mais recentes da nuvem.

## Sobre segurança

As regras do Firestore que você colou permitem que qualquer pessoa com o link do site (não do banco) leia e grave os dados — não exigem login. Isso é simples e funciona bem para uso familiar, mas tecnicamente qualquer pessoa que descobrisse o `projectId` poderia acessar os dados também. Se no futuro você quiser exigir login (ex: com e-mail e senha) antes de editar, é possível adicionar isso com o Firebase Authentication — é só avisar.
