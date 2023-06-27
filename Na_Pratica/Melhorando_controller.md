# Melhorando o controller de listagem de tarefas

Como vimos na mensagem de erro do modulo anterior não temos definido a variavel `@todos` para iterar e mostrar na tela com a nossa view.

O que precisamos entender primeiro é como o rails comunica entre controller e views, no caso utilizamos [variaveis de instancia](https://www.campuscode.com.br/conteudos/variaveis-e-self-em-ruby) que o framework automatica injeta ao renderizar a view.

Entendendo isso podemos ter nosso controller simples da seguinte forma:

```ruby
class TodoController < ApplicationController
  def index
    @todos = Todo.all
  end
end
```

Muito simples certo? a unica parte nova nessa classe é o uso do método `all` da classe `Todo` certo? Como ja vimos em modulos anteriores essa é a nossa entidade que utiliza `ActiveRecord` para comunicar com o banco de dados nessa tabela específica.

O método `all` nesse contexto retorna todas os registros da tabela "todo" na nossa aplicação e injeta na variavel de instancia para ser mostrada na view.

Agora visualizando a pagina veremos algo sendo mostrado corretamente 🚀:

![Pagina de listagem de tarefa carregando corretamente](./imgs/IMG-19-06-2023-18-54-51.png)

Parabéns! Oficialmente temos a página de listagem de tarefas funcionando corretamente.

## Trabalhando nas outras rotas

Agora vamos continuar trabalhando um pouco no controller para virmos como podemos implementar as outras rotas definidas no modulo [O que vamos construir](/Na_Pratica/O_que_vamos_construir.md)

### Rota para visualizar uma tarefa unica

Para checar por exemplo a descrição de uma tarefa ou qualquer outro tipo de informação especifica de uma tarefa, poderiamos ter um botão que ao clicar leva o usuário para aquela tarefa especifica certo?

Podemos conseguir isso com uma rota `GET /tasks/:id` ou em termos simples uma rota `show`, que podemos definir de forma simples como mostrado abaixo:

```ruby
class TodoController < ApplicationController
  def show
    @todo = Todo.find(params[:id])
  end
end
```

Aqui podemos ver alguns novos conceitos novamente:

- O método `find` existe por padrão em classes ActiveRecord e recebe um ID(numérico ou string no caso de UUIDs) retornando uma instância de entidade.
- O objeto `params` é automaticamente injetado em controllers e é um hash contendo tudo o que o usuário envia para essa rota (seja pelo body, por query param, por path param, etc).

### Rota para criar uma nova tarefa

Agora vamos definir uma rota para cadastrar uma nova tarefa onde o estado `done` sera false por padrão, dessa forma o usuário pode sempre criar uma tarefa para fazer e depois clicar para marcar como feito.

Para isso vamos definir um método `create` que vai manipular o objeto `params` ja visto antes para retornar uma nova instancia da nossa entidade de tarefa.

```ruby
class TodoController < ApplicationController
 def create
   todo = Todo.new({
     title: todo_params[:title],
     description: todo_params[:description],
     done: false
   })

   if todo.save
     redirect_to todo_path(todo)
   else
     render :new
   end
 end

 private

 def todo_params
   params.require(:title).require(:description).permit(:title, :description)
 end
end
```

Agora temos muito mais código! vamos checar com calma tudo o que foi apresentado:

1. Temos um novo método `todo_params` que manipula o objeto `param` visto anteriormente

   1. Nas multiplas chamadas do método `require` estamos dizendo para o rails que esses campos **precisam** estar presentes nos dados enviados a essa rota, caso não for enviado vamos disparar um erro de paramêtro.
   2. Na ultima chamada do método `permit` estamos dizendo para o rails limpar o objeto que foi enviado e retornar apenas as keys que estamos passando, dessa forma montamos um objeto muito mais coeso e evitamos lidar com informações desnecessárias nas nossas rotas.

2. Dentro do if onde checamos se `todo.save` ocorreu corretamente temos dois caminhos
    1. Se tudo ocorreu corretamente, fazemos uma chamada para um método builtin [redirect_to](https://apidock.com/rails/ActionController/Base/redirect_to) que redireciona o usuário para a rota `/todo/:id`, podemos perceber que o rails também proporciona um método utilitario baseado nas nossas rotas definidas no arquivo `routes.rb`, o método `todo_path` pode ser chamado sem argumentos para apontar na rota `/todo/` ou passar uma instancia de Todo tornando assim em uma rota segmentada por ID.
    2. Se algo deu errado, fazemos uma chamada para um método builtin [render](https://apidock.com/rails/ActionController/Base/render) que renderiza para o usuário o formulário de nova tarefa denovo.

#### Mas afinal, o que é a rota "new" que renderizamos caso ocorra algum erro?

Como o rails é um framework full stack, estamos lidando tanto com as rotas relacionadas com backend quanto as rotas relacionadas a frontend, nesse caso o nosso método `create` lida com o lado backend e teremos um método `new` que serve apenas para renderizar uma view especifica de formulário para a criação de um todo.

## Rota para mudar uma tarefa entre feito e não feito

Essa ação do usuário será uma rota dedicada que permitirá o usuário alterar o estado de uma tarefa entre feito e não feito (campo booleano).

Para isso vamos definir um método `toggle_done` que vai atualizar um todo apenas com a informação `done`.

```ruby
class TodoController < ApplicationController
  def toggle_done
    @todo = Todo.find(params[:id])

    @todo.update(done: !@todo.done)

    redirect_to todo_path
  end
end
```

Aqui temos uma simples negação da propriedade `done` que procuramos pelo id do
todo, assim podemos sempre ficar trocando entre `true` e `false`. Como podemos
perceber também não fazemos um condicional nesse caso, justamente porque
independente de ter dado certo ou errado vamos enviar o usuário para a pagina
de listagem de todos, dessa forma vai ser mostrado visualmente se foi alterado
ou não.

## Rota para atualizar uma tarefa

Agora vamos definir uma rota para atualizar uma tarefa já existente, nesse caso vamos permitir a atualização apenas do nome ou da descrição pois teremos uma rota dedicada para trocar entre feito e não feito.

Para isso vamos definir um método `update` que vai utilizar os paramêtros para atualizar as informação permitidas.

```ruby
class TodoController < ApplicationController
  def update
    @todo = Todo.find(params[:id])

    if @todo.update(todo_params)
      redirect_to todo_path
    else
      render :edit
    end
  end

  private

  def todo_params
    params.require(:title).require(:description).permit(:title, :description)
  end
end
```

Aqui não temos muita coisa nova, apenas uma combinação dos métodos anteriores como podemos ver no uso do `Todo.find(params[:id])`, pela definição idêntica do método `todo_params` e finalmente do condicional entre `redirect_to` e `render` em uma rota apenas para frontend (semelhante ao `:new`)

> Vale ressaltar que estamos utilizando o `todo_path` sem nenhum parametro, que indica justamente como queremos enviar para a pagina de listagem de todos.

## Rota para excluir uma tarefa

Agora vamos definir a ultima rota que irá excluir uma tarefa já existente.

Para isso vamos definir um metodo `destroy` que vai primeiro achar um todo pelo seu ID e depois exclui-lo.

```ruby
class TodoController < ApplicationController
  def destroy
    @todo = Todo.find(params[:id])

    @todo.destroy

    redirect_to todos_path
  end
end
```

Aqui semelhante ao metodo proposto para trocar o estado do todo, não precisamos
fazer um condicional pois independente do resultado vamos redirecionar o
usuário para a tela que lista os todos onde visualmente será possivel ver se
foi de fato excluido ou não.
