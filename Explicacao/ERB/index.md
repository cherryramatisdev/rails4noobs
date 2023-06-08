# O que é ERB?

ERB é uma sigla para "Embedded Ruby" e serve para incluirmos codigo ruby em N tipos de arquivo a fins de template (podemos por exemplo gerar arquivos de configuração dinamicamente usando ERB). No caso do ruby on rails é usado para manipular arquivos HTML que são usados nas nossas views dando mais poder para quem esta desenvolvendo (podendo utilizar condicionais, estruturas de repetição, classes utilitarias da aplicação, etc....)

Vamos ver mais a fundo sobre ERB nos capitulos seguintes da view, mas abaixo podemos ver um breve exemplo do que é possivel fazer com erb:

```erb
<ul>
    <% @tarefas.each do |tarefa| %>
        <li>
            <%= tarefa %>
        </li>

        <% if tarefa == "Tarefa 3" %>
            <li>Tarefa 3 lidada especificamente</li>
        <% end %>
    <% end %>
</ul>
```

Para voltar ao capitulo de views: [Criando a primeira view](/Na_Pratica/Criando_a_primeira_view.md)
