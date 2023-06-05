# Criando o primeiro modelo

Com o projeto já criado vamos começar olhando para nossas entidades, no caso
específico do nosso projeto teremos apenas uma entidade que será a `Task`, ela
vai conter um título, uma breve descrição, a informação se ela esta finalizada
ou não, e a data que ela foi inserida pelo usuário (dessa forma podemos mostrar
as mais recentes primeiro).

Dito isso vamos a prática! Entre na pasta do seu projeto e execute o seguinte comando para criar um novo modelo.

```sh
rails generate model todo title:string description:text done:boolean
```

Logo após para que de fato apliquemos nossas mudanças no banco de dados execute:

```sh
rails db:migrate
```

### Entendendo o comando passo a passo

O subcomando `generate` no rails te permite gerar [código boilerplate](https://pt.stackoverflow.com/questions/10575/o-que-%C3%A9-boilerplate-code) de coisas comuns do dia a dia (como controllers, models, migrations, views, mailers, etc...) com mais facilidade. Um adendo, bibliotecas de terceiros também podem instalar novos generators no seu projeto para facilitar mais ainda a configuração.

> Para checar todos os generators presentes no seu projeto, basta executar rails generate --help na raiz do projeto.

### O que geramos?

Após executar esse comando, um output foi printado na tela com os arquivos que foram criados, algo parecido com isso:

```sh
λ rails generate model todo title:string description:text done:boolean                  [main] ~/Repos/todo4noobs
      invoke  active_record
      create    db/migrate/20230530214600_create_todos.rb
      create    app/models/todo.rb
      invoke    test_unit
      create      test/models/todo_test.rb
      create      test/fixtures/todos.yml
```

Podemos ver um arquivo na pasta db chamado `20230530214600_create_todos.rb`, mas o que isso significa?

Bom, um arquivo de migração serve para que possamos construir nossa base de
dados gradativamente, você deve perceber o ID numérico que ficou na frente do
nome do arquivo `20230530214600` certo? esse identificador serve justamente
para que o rails([active
record](https://guides.rubyonrails.org/active_record_basics.html)) registre quais migrações ja foram executadas e quais ainda precisam ser executadas, dessa forma uma migração **nunca é executada duas vezes**.

Também podemos observar o arquivo `app/models/todo.rb`, que como vimos no capitulo sobre [MVC](/Arquitetura/MVC.md), representa a camada de representação e integração com banco de dados na nossa aplicação.

Como o rails é um framework
[TDD](https://www.treinaweb.com.br/blog/afinal-o-que-e-tdd), ele também ja as
pastas e arquivos necessários para conseguirmos definir
[mocks](https://www.devmedia.com.br/mocks-introducao-a-automatizacao-de-testes-com-mock-object/30641)
e testar esse novo model.

### Próximos passos

A partir de agora não vamos usar tantos generators visto que vamos criar arquivos de regra de negócio como controllers, views, etc...

Agora vamos criar nosso primeiro controller e devolver um texto simples já fazendo query no banco! também vamos conhecer um pouco mais sobre o console interativo do rails. [Criando o primeiro controller](/Na_Pratica/Criando_o_primeiro_controller.md)
