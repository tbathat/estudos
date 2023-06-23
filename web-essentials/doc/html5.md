O site usa o ChakraUI, o cockpit novo usa, hcondo, paghouse.

# HTML5 (semântico)

## TAGS ESTRUTURAIS (também conhecidas como **elements**)

- Main: só pode haver uma `main` e ela é a parte principal da página. Ela fica somente dentro do `body` e todos os demais elmentos vão dentro dela, como `header`, `section`, `span`, `footer`e etc.

1. Importante: as tags `header`, `footer` podem ficar fora da main.
2. Importante: ela também não pode ter `input`ou ferramenta de busca.

- <header>: é usada para conteúdos introdutórios ou para um set de links para navegação.
- <Footer>: elementos de rodapé (endereço, copyright, etc)
- <Section>: no exemplo de uma busca por casas para alugar, quando aparecer os resultados, cada caso com suas informações específicas é uma section. Podemos fazer analogia com a div, mas ela é genérica.
  Ela é contraindicada para indexação. O intuito do section é ser uma seção de informações relacionadas ao conteúdo que está navegando.
- <Aside>: é um assunto que não tem a ver com o assunto principal daquela página. No exemplo do site de busca de casas para alugar, você pode colocar no aside informações como: fale com o corretor, fazer anúncios, classificados, etc. É relegado à assuntos "auxiliares".

1. ELa pode abraçar outras seções.

- <Div>: Quando é somente um propósito de estilização, porque é completamente genérica.
- <Nav>: é utilizado para o menu de navegação.

1. Se você incluir `<nav>` dentro do `Header` vai ficar sub-entendido para o web scrap que é a navegação dentro do cabeçalho.
2. Se você incluir `<nav>` dentro do `Footer`, vai ficar sub-entendido para o web scrap que é a navegação dentro do rodapé.

- <Article> A tag `<article>` especifica um conteúdo independente e autocontido. Um artigo deve ter sentido por si só e deve ser possível distribuí-lo independentemente do restante do site.

Fontes potenciais para o elemento <article>:

- Postagens de fórum
- Posts de blog
- Notícias

Ou seja, o `<article>` é direcionado à colocar o conteúdo relacionado à página. Ele tem uma característica de `aninhamento`, onde podemos colocar um dentro do outro.

Exemplo:

```
<article>
     <p>Qual seu prato favorito?</p>
     <article>
          <p>Churrasco</p>
     </article>
</article>
```

Isso faz com que os mecanismos de busca entenda que o article filho está relacionado ao pai, então o web scrapping vai entender a relação html.

MACETE:

- Se eu esrever `nav>ul>li>*3>a` e der um `tab`, ele vai criar:

<nav>
     <ul>
          <li<>a href:="#">Item 1</li>
          <li><a href:="#">Item 2</li>
          <li><a href:="#">Item 3</li>
     </ul>
</nav>

- Vá em `inspecionar` para checar a estrutura DOM.
