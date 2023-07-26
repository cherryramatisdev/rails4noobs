# Melhorando nossas views

Como rails é um framework fullstack que cuida tanto da parte backend quanto frontend ele nos permite definir rotas para nosso backend com todos os argumentos que sabemos (GET, POST, PUT, etc...) e também permite que definimos rotas estritamente para carregar nossas views (essas rotas são apenas get).

Então ao analisarmos um de nossos métodos que criamos no capitulo anterior podemos ver o seguinte:

Esse método carrega o nome `create` por um motivo especifico, normalmente em aplicações rails nós criamos pares de método com nomenclaturas especificas

- new / create
- edit / update

We can see that the method `new` represents the frontend(a GET that render the view) and the `create` represents the backend(a POST that perform database actions), this also can be said for `edit`(frontend) and `update`(backend)

```ruby
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
```

With that in mind let's define our routes so we can start working on the views:

On our controller file:

```ruby
class TodoController < ApplicationController
  def new
    @todo = Todo.new
  end

  def edit
    @todo = Todo.find(params[:id])
  end
end
```

Just to make sure let's break down how these methods work:

1. The method `new` just instantiate a `Todo` model so we can use on the form (we'll see in detail later)
2. The method `edit` get the id from the URL like `/todo/1` and use this to find the correct todo e provide as a variable for the template, this help us provide the edit form with pre filled information for the user
