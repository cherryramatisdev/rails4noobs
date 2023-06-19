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

Muito simples certo? a unica parte nova nessa classe é o uso do metodo `all` da classe `Todo` certo? Como ja vimos em modulos anteriores essa é a nossa entidade que utiliza `ActiveRecord` para comunicar com o banco de dados nessa tabela específica.

O metodo `all` nesse contexto retorna todas os registros da tabela "todo" na nossa aplicação e injeta na variavel de instancia para ser mostrada na view.

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

Agora podemos ver alguns novos conceitos novamente:

- O metodo `find` existe por padrão em classes ActiveRecord e recebe um ID(numérico ou string no caso de UUIDs) retornando uma instância de entidade.
- O objeto `params` é automaticamente injetado em controllers e é um hash contendo tudo o que o usuário envia para essa rota (seja pelo body, por query param, por path param, etc).
