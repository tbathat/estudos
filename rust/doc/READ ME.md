Esse conteúdo foi desenvolvido exclusivamente com o intuito de estudos pessoais, com base na documentação original do Rust e materiais complementares.

O Rust é uma linguagem de tipagem estática, o que significa que ela não permite alterar o tipo da variável
após ela ser tipada. Essa verificação é feita em tempo de compilação, por isso é possível inferir o tipo
da variável baseado no valor que foi atribuído.

Uma vez que o tipo é inferido, não é possível alterá-lo.

Por isso o Rust tem: tipagem estática, inferida e fortemente tipada (o que significa que não podemos realizar
conversões de tipo automaticamente).

- O Rust tem vários tipos primitivos porque embutiu os modificadores.

- Por exemplo: só para os tipos inteiros, são 12 variações (vai de 8 à 128 bits) podendo ser `signed` ou `unsigned`, algo que delimita o `range` de valores e é tem como finalidade `indexar o tipo de coleção`.

- Outro ponto, existe o `arch` onde o tamanho do tipo de dado será definido de acordo com a arquitetura da máquina. Ela é definida usando o `isize` e o `usize`. Isso garante que eles terão o tamanho suficiente para armazenamento dependendo da arquitetura.
