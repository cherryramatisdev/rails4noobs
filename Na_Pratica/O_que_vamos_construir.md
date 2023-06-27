# O que vamos construir?

Como o foco desse tutorial é garantir o aprendizado do framework ruby on rails, vamos apostar em um projeto simples que vai nos permitir construir um CRUD e visualizar as funcionalidades basicas de uma aplicação web fullstack.

Dito isso vamos construir uma simples todo list, dessa forma podemos observar como o rails provê habilidades de reatividade no frontend usando [hotwire](https://hotwired.dev/).

Rotas que teremos:

> Caso tenha dificuldade entendendo o conceito de CRUD e metodos basicos do HTTP, recomendo ler aqui: <TODO: LINKA AQUI>

- GET /todos
- GET /todos/:id
- POST /todos
- PUT /todos/:id/toggle
- PUT /todos/:id
- DELETE /todos/:id

Nessa proposta acima, a unica rota que divergimos do CRUD padrão é a `/todos/:id/toggle` que vai permitir o usuário alterar uma tarefa entre feito e não feito, estamos escolhendo essa decisão para tornar nossa API mais declarativa e separada quanto a regras de negócio.
