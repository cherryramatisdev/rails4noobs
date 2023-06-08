# Condicionais

Como ja falamos no [Diferença entre tag de exibição e tag de controle](/Explicacao/ERB/Diferenca_entre_tag_de_exibicao_e_tag_de_controle.md), podemos utilizar as tags de controle para criar condicionais em nossos templates, essas condicionais podem ter os seguintes tipos (que seguem a linguagem ruby visto que ERB é apenas um Embedded Ruby).

- If

Ja vimos algumas vezes o if e com ele podemos construir condicionais unicos ou multiplos considerando primeiro o caminho `true` e depois o caminho `false`, como mostrado abaixo:

```erb
<% if "todo".empty? %>
  <h1>todo não foi encontrado</h1>
<% else %>
  <h1>todo foi encontrado</h1>
<% end %>
```

> Isso vai produzir um h1 escrito "todo foi encontrado" na tela.

- Unless

O unless se comporta da mesma forma que o if, mas com ele podemos assumir o caminho `false` primeiro e depois o caminho `true`, como mostrado abaixo:

```erb
<% unless "todo".empty? %>
  <h1>todo não foi encontrado</h1>
<% else %>
  <h1>todo foi encontrado</h1>
<% end %>
```

> Isso vai produzir um h1 escrito "todo não foi encontrado" na tela.

- Case

No caso desse condicional conhecido como switch em outras linguagens como javascript, podemos analisar uma unica variável por multiplos angulos como mostrado abaixo:

```erb
<% case 1 %>
<% when 0 %>
  <h1>É zero</h1>
<% when 1 %>
  <h1>É um</h1>
<% else %>
  <h1>É qualquer outro número</h1>
<% end %>
```

> Isso vai produzir um h1 escrito "É um" na tela.
