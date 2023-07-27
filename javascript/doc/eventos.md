# Eventos Javascript

No caso da web, eventos são disparados dentro da janela do navegador, e tende a estarem anexados a algum item especifico nele — pode ser um único elemento, um conjunto de elementos, o HTML carregado na guia atual, ou toda a janela do navegador.

Existem vários tipos diferentes de eventos que podem vir a acontecer.

> Event handler: Cada evento disponivel possui um manipulador de eventos (event handler).

É um bloco de código (geralmente uma função JS definida pela programadora) que será executado quando o evento for disparado pelo usuário. Quando esse bloco de código é definido para rodar em resposta a um evento que foi disparado no lado do cliente (usuário), nós dizemos que estamos registrando um manipulador de eventos (event handler).

_Os ouvintes (event lister) escutam o evento acontecendo, e o manipulador (event handler) é o codigo que roda em resposta a este acontecimento_.

## Convenções

## Formas de usar eventos da web

Há várias maneiras diferentes de adicionar código de ouvinte de evento a páginas da Web para que ele seja executado quando o evento associado for disparado.

### Propriedades do manipulador de eventos

- Essas são as propriedades que existem para conter o código do manipulador de eventos que vimos com mais frequência durante o curso.

Exemplo 1:

```
var btn = document.querySelector("button");

btn.onclick = function () {
  var rndCol =
    "rgb(" + random(255) + "," + random(255) + "," + random(255) + ")";
  document.body.style.backgroundColor = rndCol;
};
```

A propriedade `onclick` é a propriedade do manipulador de eventos que está sendo usada nesta situação. É essencialmente uma propriedade como qualquer outra disponível no botão (por exemplo, btn.textContent, ou btn.style (en-US)), mas é um tipo especial — quando você configura para ser igual a algum código, esse código será executado quando o evento é acionado no botão.

- Você também pode definir a propriedade handler para ser igual a um nome de função nomeado (como vimos em Construa sua própria função).

O seguinte funcionaria da mesma forma. Exemplo 2:

``
var btn = document.querySelector("button");

function bgChange() {
var rndCol =
"rgb(" + random(255) + "," + random(255) + "," + random(255) + ")";
document.body.style.backgroundColor = rndCol;
}

btn.onclick = bgChange;

```

### Evite manipuladores in-line
```

html

<button onclick="alert('Hello, this is my old-fashioned event handler!');">
  Press me
</button>
```

- Você encontrará equivalentes de atributo HTML para muitas das propriedades do manipulador de eventos; no entanto, você não deve usá-los — eles são considerados uma prática ruim.

- Pode parecer fácil usar um atributo manipulador de eventos se você estiver apenas fazendo algo realmente rápido, mas eles se tornam rapidamente incontroláveis e ineficientes.

- Para começar, não é uma boa ideia misturar o seu HTML e o seu JavaScript, pois é difícil analisar — manter seu JavaScript em um só lugar é melhor; se estiver em um arquivo separado, você poderá aplicá-lo a vários documentos HTML.

\*DICA: Acessar a documentação da mozilla para

_NOTA: Separar sua lógica de programação do seu conteúdo também torna seu site mais amigável aos mecanismos de pesquisa._

## Event Listeners | addEventListener() e removeEventListener()

> addEventListener(): Este método é usado para adicionar um ouvinte (listener) a um elemento específico. Um ouvinte é uma função que será executada quando um evento ocorrer no elemento. Os eventos podem ser coisas como cliques do mouse, pressionamento de teclas, submissão de formulários, carregamento de páginas, entre outros. Você pode usar addEventListener() para "ouvir" esses eventos em um elemento HTML e realizar ações em resposta a eles.

```
const meuBotao = document.getElementById('meu-botao');

function acaoDoBotao() {
  alert('O botão foi clicado!');
}
```

meuBotao.addEventListener('click', acaoDoBotao);

> removeEventListener(): Este método é usado para remover um ouvinte previamente adicionado de um elemento. Às vezes, você pode querer desativar temporariamente um ouvinte ou removê-lo permanentemente. Para fazer isso, você precisa usar removeEventListener() e passar o mesmo tipo de evento e a mesma função do ouvinte que você usou anteriormente.

```
const meuBotao = document.getElementById('meu-botao');

function acaoDoBotao() {
  alert('O botão foi clicado!');
  meuBotao.removeEventListener('click', acaoDoBotao);
}

meuBotao.addEventListener('click', acaoDoBotao);
```

Algumas possibilidades de uso incluem:

- Validação de formulários: Ao ouvir o evento de envio de formulários, você pode validar os campos antes de permitir que o usuário envie os dados.
- Navegação de página: Usando eventos de clique, você pode criar botões ou links que alteram a visualização da página.
- Manipulação de elementos: Eventos como arrastar e soltar (drag and drop) podem ser usados para reorganizar elementos na página.
- Respostas a ações do usuário: Por exemplo, ao clicar em um botão, você pode adicionar ou remover itens em uma lista.
- Interação com animações: Você pode disparar animações em resposta a eventos, como uma transição quando um elemento é clicado.

Essas são apenas algumas das muitas possibilidades que addEventListener() e removeEventListener() oferecem para desenvolvedores web, tornando a experiência do usuário mais rica e interativa.

### VISÃO GERAL SOBRE OS MANIPULADORES DE EVENTOS

Dentro da função addEventListener(), especificamos dois parâmetros — o nome do evento para o qual queremos registrar esse manipulador, e o código que compreende a função do manipulador que queremos executar em resposta a ele. Note que é perfeitamente apropriado colocar todo o código dentro da função addEventListener(), em uma função anônima, assim:

```
js

btn.addEventListener("click", function () {
  var rndCol =
    "rgb(" + random(255) + "," + random(255) + "," + random(255) + ")";
  document.body.style.backgroundColor = rndCol;
});
```

Em segundo lugar, você também pode registrar vários manipuladores para o mesmo ouvinte. Os dois manipuladores a seguir não seriam aplicados:

```
js

myElement.onclick = functionA;
myElement.onclick = functionB;
```

Como a segunda linha sobrescreveria o valor de onclick definido pelo primeiro. Isso funcionaria, no entanto:

```
js

myElement.addEventListener("click", functionA);
myElement.addEventListener("click", functionB);
```

Ambas as funções serão executadas quando o elemento for clicado.

Além disso, há vários outros recursos e opções poderosos disponíveis com esse mecanismo de eventos.
Há muitas propriedades diferentes de manipulador de eventos disponíveis.

### Qual mecanismo de manipulação escolher?

As principais vantagens do último mecanismo são que você pode remover o código do manipulador de eventos, se necessário, usando removeEventListener(), e você pode adicionar vários listeners do mesmo tipo aos elementos, se necessário.
Por exemplo, você pode chamar addEventListener('click', function() { ... }) em um elemento várias vezes, com diferentes funções especificadas no segundo argumento. Isso é impossível com as propriedades do manipulador de eventos porque qualquer tentativa subseqüente de definir uma propriedade sobrescreverá as anteriores, por exemplo:

```
element.onclick = function1;
element.onclick = function2;
etc.
```

## Outros conceitos de evento

### Objetos de evento

- Às vezes, dentro de uma função de manipulador de eventos, você pode ver um parâmetro especificado com um nome como event, evt, ou simplesmente e. Isso é chamado de event object, e é passado automaticamente para os manipuladores de eventos para fornecer recursos e informações extras. Por exemplo, vamos reescrever nosso exemplo de cor aleatória novamente:

```

function bgChange(e) {
  var rndCol =
    "rgb(" + random(255) + "," + random(255) + "," + random(255) + ")";
  e.target.style.backgroundColor = rndCol;
  console.log(e);
}
btn.addEventListener("click", bgChange);
```

Quando você adiciona um ouvinte a um elemento usando addEventListener(), uma instância de objeto de evento é criada e passada como argumento para a função do ouvinte quando o evento ocorre. Este objeto contém informações relevantes sobre o evento que ocorreu. Aqui estão algumas informações importantes sobre objetos de evento:

1.  Propriedades do objeto de evento: O objeto de evento contém várias propriedades que fornecem informações sobre o evento. Algumas das propriedades comuns incluem:

- event.type: O tipo de evento que ocorreu (por exemplo, "click", "keydown", "submit", etc.).
- event.target: O elemento HTML em que o evento foi originalmente acionado (ou seja, o elemento alvo do evento).
- event.clientX e event.clientY: As coordenadas do cursor do mouse no momento em que o evento ocorreu (aplicável a eventos de mouse).
- event.key: A tecla que foi pressionada (aplicável a eventos de teclado).
- event.preventDefault(): Um método que pode ser usado para evitar o comportamento padrão do evento (por exemplo, evitar o envio de um formulário ou o link de navegação).

```
const meuBotao = document.getElementById('meu-botao');

function acaoDoBotao(event) {
event.preventDefault(); // Evita que o formulário seja enviado (se o botão estiver dentro de um formulário)
console.log('Evento:', event.type);
console.log('Elemento alvo:', event.target);
console.log('Coordenadas X do mouse:', event.clientX);
console.log('Coordenadas Y do mouse:', event.clientY);
}

meuBotao.addEventListener('click', acaoDoBotao);
```

_DICA_: e.target é incrivelmente útil quando você deseja definir o mesmo manipulador de eventos em vários elementos e fazer algo com todos eles quando ocorre um evento neles. Você pode, por exemplo, ter um conjunto de 16 blocos que desaparecem quando são clicados.

# Mais sobre:

- Eventos (Event): A interface de eventos representa qualquer evento de DOM. Ele contém propriedades comuns e métodos para qualquer evento. Disponível em: https://developer.mozilla.org/pt-BR/docs/Web/API/Event.

- Event Listeners: Disponível em: https://developer.mozilla.org/pt-BR/docs/Web/API/EventTarget/addEventListener.

- API JAVASCRIPT: Disponível em: https://developer.mozilla.org/en-US/docs/Web/API/Element

<!-- TODO: Ler e registrar sobre eventos em nodejs no lado do servidor (https://nodejs.org/docs/latest-v5.x/api/events.html)
Eventos http em node: https://nodejs.org/docs/latest-v8.x/api/http.html#http_event_connect -->

<!-- # DOM

- Document
- Window
- Elements -->


