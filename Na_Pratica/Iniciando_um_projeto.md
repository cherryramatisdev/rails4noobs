# Iniciando um projeto

Para iniciar um projeto com ruby on rails abra um terminal em alguma pasta onde guarda os seus projetos e execute o seguinte comando:

```sh
rails new rails4noobs # rails4noobs é o nome do projeto, pode escolher qualquer um
```

Executando esse comando você terá estrutura parecida com a mostrada abaixo:

```
/tmp/todos/
├── Gemfile
├── Gemfile.lock
├── README.md
├── Rakefile
├── app
│   ├── assets
│   │   ├── config
│   │   │   └── manifest.js
│   │   ├── images
│   │   └── stylesheets
│   │       └── application.css
│   ├── channels
│   │   └── application_cable
│   │       ├── channel.rb
│   │       └── connection.rb
│   ├── controllers
│   │   ├── application_controller.rb
│   │   ├── concerns
│   │   └── todos_controller.rb
│   ├── helpers
│   │   ├── application_helper.rb
│   │   └── todos_helper.rb
│   ├── javascript
│   │   ├── application.js
│   │   └── controllers
│   │       ├── application.js
│   │       ├── hello_controller.js
│   │       └── index.js
│   ├── jobs
│   │   └── application_job.rb
│   ├── mailers
│   │   └── application_mailer.rb
│   ├── models
│   │   ├── application_record.rb
│   │   ├── concerns
│   │   └── todo.rb
│   └── views
│       ├── layouts
│       │   ├── application.html.erb
│       │   ├── mailer.html.erb
│       │   └── mailer.text.erb
│       └── todos
│           └── index.html.erb
├── bin
│   ├── bundle
│   ├── importmap
│   ├── rails
│   ├── rake
│   └── setup
├── config
│   ├── application.rb
│   ├── boot.rb
│   ├── cable.yml
│   ├── credentials.yml.enc
│   ├── database.yml
│   ├── environment.rb
│   ├── environments
│   │   ├── development.rb
│   │   ├── production.rb
│   │   └── test.rb
│   ├── importmap.rb
│   ├── initializers
│   │   ├── assets.rb
│   │   ├── content_security_policy.rb
│   │   ├── filter_parameter_logging.rb
│   │   ├── inflections.rb
│   │   └── permissions_policy.rb
│   ├── locales
│   │   └── en.yml
│   ├── master.key
│   ├── puma.rb
│   ├── routes.rb
│   └── storage.yml
├── config.ru
├── db
│   ├── development.sqlite3
│   ├── migrate
│   │   └── 20230523222051_create_todos.rb
│   ├── schema.rb
│   └── seeds.rb
├── lib
│   ├── assets
│   └── tasks
├── log
│   └── development.log
├── public
│   ├── 404.html
│   ├── 422.html
│   ├── 500.html
│   ├── apple-touch-icon-precomposed.png
│   ├── apple-touch-icon.png
│   ├── favicon.ico
│   └── robots.txt
├── storage
├── test
│   ├── application_system_test_case.rb
│   ├── channels
│   │   └── application_cable
│   │       └── connection_test.rb
│   ├── controllers
│   │   └── todos_controller_test.rb
│   ├── fixtures
│   │   ├── files
│   │   └── todos.yml
│   ├── helpers
│   ├── integration
│   ├── mailers
│   ├── models
│   │   └── todo_test.rb
│   ├── system
│   └── test_helper.rb
└── vendor
    └── javascript

46 directories, 68 files
```

Como pode ver o projeto padrão te entrega **muita** coisa e isso esta completamente de acordo com a filosofia [Convention Over Configuration](../Arquitetura/Convention_over_Configuration). Vamos entender agora no detalhe o que cada nivel de pasta significa para o framework.

## Entendendo a estrutura de arquivos

A estrutura de um projeto Rails apresentada acima segue a convenção padrão do framework Ruby on Rails. Vamos descrever cada diretório e arquivo e seu propósito dentro do projeto:

- `Gemfile`: É um arquivo que define as dependências do projeto e as versões das mesmas.
- `Rakefile`: Rake é uma ferramenta de automação do ruby que permite definir scripts uteis para criação de arquivos (controllers, testes, etc...) por exemplo e o Rakefile justamente define cada uma dessas tarefas (vamos ver mais delas em detalhe no capitulo [Comandos do rails](Na_Pratica/Comandos_do_rails.md).
- `app`: É o diretório principal onde a lógica da aplicação reside.
  - `assets`: É o diretório que contém os recursos estáticos da aplicação, como folhas de estilo (CSS), imagens e JavaScript.
  - `channels`: Nesse diretório definimos as classes responsaveis por [respostas em tempo real](https://guides.rubyonrails.org/action_cable_overview.html)
  - `controllers`: Nesse diretório definimos as classes que lidam com requisições HTTP ([relembre o modelo MVC](Arquitetura/MVC.md))
  - `helpers`: Nesse diretório vão ser definidas as classes utilitarias que podem ser usadas em multiplos lugares da aplicação (inclusive em views!)
  - `javascript`: Nesse diretório são armazenados todo o javascript necessário tanto para a execução minima do rails quanto para futuras bibliotecas utilitárias que queiramos usar (sim, tem como colocar frameworks complexos como [React](https://medium.com/rd-shipit/how-to-set-up-a-rails-7-project-with-react-and-jest-f2e016bfbdf3) em um projeto rails)
  - `jobs`: Nesse diretório vão ser definidas as classes para declarar jobs (tarefas que executam em um momento X e que normalmente são controladas por uma [fila de execução](https://www.geeksforgeeks.org/queue-data-structure/))
  - `mailers`: Nesse diretório vão ser definidas as classes responsáveis por enviar emails transacionais, podemos tanto definir emails simples de texto como emails com layouts complexos utilizando HTML.
  - `models`: Nesse diretório vão ser definidas as entidades principais da aplicação (que também podem ser utilizadas para interagir com o banco de dados)
  - `views`: Nesse diretório vão ser definidos os arquivos HTML que servirão como a camada final que o usuário vai ver no navegador ao acessar nosso serviço.
- `bin`: É o diretório que contém os scripts executáveis relacionados ao projeto.
- `config`: Contém toda configuração relacionada a variavel de ambiente, definição de rotas(rails considera isso como configuração), credenciais de banco de dados e outros metodos de armazenamento, etc...
- `config.ru`: Arquivo de configuração do Rack, usado pelo servidor web para iniciar a aplicação.
- `db`: Nesse diretório vão ficar todos os arquivos relacionados a banco de dados como arquivos de migração(mais detalhes em [Migrações](Na_Pratica/Migrações.md))
- `lib`: É o diretório que contém bibliotecas ou módulos adicionais.
- `log`: É o diretório que contém os logs de execução da aplicação, muito util para entender eventuais problemas durante a execução do nosso projeto.
- `public`: É o diretório público da aplicação, acessível diretamente pelo navegador. <https://www.techopedia.com/definition/15605/public-folder>
- `storage`: Nesse diretório ficam os arquivos gerados por modulos de upload de arquivo (aqueles formularios de "arraste o arquivo para ca") para facilitar os testes locais.
- `test`: É o diretório que contém os testes da aplicação, dentro desse diretório teremos testes de feature, testes unitários e por ai vai.
- `vendor/`: Nesse diretório fica um cache de bibliotecas externas (normalmente javascript como jquery).

Próximo: [Criando o primeiro modelo](Na_Pratica/Criando_o_primeiro_modelo.md)
