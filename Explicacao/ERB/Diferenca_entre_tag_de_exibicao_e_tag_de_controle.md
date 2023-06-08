# Diferença entre tag de exibição e tag de controle

Utilizando erb temos duas formas de utilizar a linguagem ruby dentro do html:

- Exibindo algum conteúdo para o usuário final (tela do navegador):

Nesse caso estamos falando de qualquer coisa que aparece na tela como uma variavel, para isso usamos o padrão `<%= %>`. Perceba que o `=` diferencia essa tag em específico, podemos por exemplo exibir o valor de uma variavel para a tela(sendo o uso mais comum): `<%= variavel %>`

- Não exibindo algum conteúdo para o usuário final

Já nesse caso estamos falando de estruturas que **não** aparecem para o usuário final, logo usamos essa tag para declarar condicionais, estruturas de repetição, etc...Por exemplo podemos usar um if com: `<% if 1 > 0 %>`, esses condicionais vão ser acompanhados de uma tag especial `<% end %>` que indica o escopo onde podemos incluir conteudo, por exemplo:

```erb
<% if 1 > 0 %>
    <h1>O valor de 1 é maior que 0</h1>
<% end %>
```
