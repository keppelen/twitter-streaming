# Como fazer deploy de uma app em Node.JS para o Heroku

## Passo 1 - Cadastro

Caso você ainda não tenha uma conta no Heroku, [crie uma agora](https://api.heroku.com/signup).

## Passo 2 - Heroku Toolbelt

Instale o cinto de utilidades do Heroku, nele você encontra: 

* Uma ferramenta para linha de comando que cria e gerencia as apps no Heroku; 
* Foreman, uma opção simples para rodar seus apps localmente;
* Git, o sistema de controle de versão necessário para fazer deploy das aplicações.

## Passo 3 - Login

Depois de instalar o cinto de utilidades, você terá acesso ao comando `heroku` através da linha de comando. Faça login usando seu email e senha da conta do Heroku.

```
$ heroku login
Enter your Heroku credentials.
Email: adam@example.com
Password: 
Could not find an existing public key.
Would you like to generate one? [Yn] 
Generating new SSH public key.
Uploading ssh public key /Users/adam/.ssh/id_rsa.pub
```

## Passo 4 - Rodando localmente

Para rodar seu processo, você precisa declarar qual comando vai utilizar. Nesse caso, nós simplesmente precisar executar nosso script. Nós iremos usar Procfile.

1. Iniciamos o controle de versão: `git init`
2. Ignoramos os módulos instalados pelo npm: `echo 'node_modules' >> .gitignore`
3. Crie um arquivo chamado Procfile: `touch Procfile`
4. E acrescente o seguinte conteúdo no arquivo: `echo 'web: node app.js' >> Procfile`
5. Agora é só sua aplicação com Foreman (instalado como parte do Heroku Toolbelt): 

```
$ foreman start
14:39:04 web.1     | started with pid 24384
14:39:04 web.1     | Listening on 5000
Your app will come up on port 5000. Test that it’s working with curl or a web browser, then Ctrl-C to exit.
```
6. Agora abra seu navegador para ver a aplicação rodando: `localhost:5000`

## Passo 5 - Deploy para o Heroku

1. Comitamos os arquivos do projeto: 

``` 
git add .
git commit -m 'initial commit'
```
2. Criamos uma nova instância no Heroku: 

```
$ heroku create --stack cedar
```

3. Deploy do nosso código: `$ git push heroku master`
4. Antes de abrirmos nossa app no browser precisamos escalar o processo: `$ heroku ps:scale web=1`
5. Para ver como anda os processos em execução: `$ heroku ps`
6. Agora é só ver como ficou no browser: `heroku open`

## Referências

* https://devcenter.heroku.com/articles/quickstart
* https://devcenter.heroku.com/articles/nodejs	
* http://robdodson.me/blog/2012/06/04/deploying-your-first-node-dot-js-and-socket-dot-io-app-to-heroku/