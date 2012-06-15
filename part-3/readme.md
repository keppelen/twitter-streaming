# Node.js - Como fazer deploy para o Heroku

Esse é o último de uma série de três artigos sobre Node.js. Não deixe de confirar os primeiros artigos da série:

* Node.js - Primeiros passos usando Express
* Node.js - Criando uma aplicação de tempo real usando Socket.io
* Node.js - Criando uma aplicação de tempo real usando Socket.io

---

Heroku é um serviço de hospedagem na nuvem absurdamente simples e extremamente escalável. Ele te dá o poder de colocar no ar aplicações Ruby, Node.js, Clojure, Java, Python ou Scala sem pagar nada e, à medida que crescerem, adicionar recursos pagando algumas doletas a mais.

Se você já é do mundo Ruby provavelmente já ouviu muito falar dele, se não prepare-se para se apaixonar pela praticidade de fazer deploy através de um simples push do Git.

## Passo 1 - Cadastro

Caso você ainda não tenha uma conta no Heroku, [crie uma agora](https://api.heroku.com/signup).

## Passo 2 - Heroku Toolbelt

Instale o [cinto de utilidades do Heroku](https://toolbelt.heroku.com/). Ele possui tudo o que você precisa para começar a brincadeira: 

* [Heroku client](http://github.com/heroku/heroku), uma ferramenta para linha de comando que cria e gerencia as apps no Heroku; 
* [Foreman](http://github.com/ddollar/foreman), uma opção simples para rodar suas apps localmente;
* [Git](http://git-scm.com), o sistema de controle de versão necessário para fazer deploy das aplicações.

## Passo 3 - Login

Depois de instalar o [cinto de utilidades](https://toolbelt.heroku.com/), você terá acesso ao comando `heroku` através da linha de comando. Faça o login usando seu email e senha da conta do Heroku.

```
heroku login
```

## Passo 4 - Rodando localmente

Para rodar seu processo, você precisa declarar qual comando vai utilizar. Nesse caso, nós simplesmente precisamos executar nosso script e quem vai cuidar disso para nós é o **Procfile**.

1. Iniciamos o controle de versão: `git init`
2. Ignoramos os módulos instalados pelo **NPM**: `echo 'node_modules' >> .gitignore`
3. Crie um arquivo chamado **Procfile**: `touch Procfile`
4. E acrescente o seguinte conteúdo no arquivo: `echo 'web: node app.js' >> Procfile`
5. Agora é só rodar sua aplicação com o **Foreman**:  `foreman start`
6. E abrir seu navegador no endereço a seguir, para ver a aplicação rodando: `localhost:5000`

## Passo 5 - Deploy para o Heroku

Agora que está rodando tudo direitinho localmente, está na hora de colocar isso online.

1. Comitamos os arquivos do projeto: 

``` 
git add .
git commit -m 'initial commit'
```
2. Criamos uma nova instância no Heroku: `heroku create --stack cedar`
3. E fazemos o deploy da nossa app: `git push heroku master`
4. Antes de abrirmos ela no navegador, precisamos escalar o processo: `heroku ps:scale web=1`
5. Para ver se está tudo bem e como andam os processos em execução: `heroku ps`
6. Agora é só ver como ficou no navegador: `heroku open`

## Referências

* https://devcenter.heroku.com/articles/quickstart
* https://devcenter.heroku.com/articles/nodejs	
* http://robdodson.me/blog/2012/06/04/deploying-your-first-node-dot-js-and-socket-dot-io-app-to-heroku/
* http://imasters.com.br/artigo/22016/javascript/o-que-exatamente-e-o-nodejs