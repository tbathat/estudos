# Formulários HTML

## Tags e atributos Form:

- <form></form> : tudo dentro dessa tag é o formulário.

- atributo `name=""`:ajuda a pegar a instância do formulário para validar no JS.

- atributo `action=""`: depois de validar os dados, esse atributo vai enviar as informações para o endereço de servidor desejado. 
Exemplo: <form action="https://localhost:3000">

> Aqui tem um porém que pode infrigir o CORS, quando você tenta enviar um formulário para um site que você não tem acesso. Por isso, existe o sistema de segurança CORS.

- atributo `method=""`: tem dois valores possíveis, o GET e POST. 

> GET: repare que os dados incluídos nos campos do formulário são atribuídos aos parâmetros do endereço no navegador.
> POST: ele não manda pela url, ele manda via body da requisição. Ou seja, ele vai estar fazendo uma requisição para o servidor.

- atributo `target=""`: se usar por exemplo, _blank, ao submeter o formulário a validação dele ocorrerá em outra aba.

- atributo `autocomplete=""` (on / off): o navegador vai manter os dados para uma outra situação de uso do formulário.

- atributo `onsubmit=""` : aqui vamos submeter um código javascript, para disparar o evento `onsubmit` ao clicar no botão. 

> Geralmente utilizado para a validação dos dados enquanto eles são inseridos pelo usuário no formulário.

## Tag input: 

- input="" : Utilizada para tudo que for escrito no formulário pelo usuário, toda informação inputada.

- Atributo `type=""`: esse atributo possui várias opções para você definir o tipo de dado, como: text, password, etc.

> `type="number" min="0" max="100" step="5"` (faz pular de 5 em 5 usando a seta do campo)

> `type="button" value="Enviar"` (pro navegador, vai aparecer um button com escrita "Enviar"). Semanticamente é incorreto, melhor utilizar a tag button e dentro atribuir type="submit", por exemplo.

> `type="range"` : você pode scrollar entre um valor min e max, e atribuir um `value=""` inicial.

> `type="date" `: cria um campo para selecionar data com base no idioma do navegador. 

> `type="file"` `multiple` : cria um campo para selecionar um arquivo. Multiple aceita vários arquivos, mas é opcional.

## Checkbox e Radio Button

*Tem uma particularidade que se não prestarmos atenção, poderá nos prejudicar no futuro.*

 > Checkbox: a ideia é selecionar múltiplos valores. Mas por conta disso, na hora de transferir para o servidor devemos falar quais valores foram selecionados. Por isso, não enviamos um a um de forma independente, vamos mandar todos de uma vez utilizando o atributo `name=""`.
 
> A ideia é que o checkbox seja:
 	1. uma variável recebendo de 1 a mais valores.
 	
 Por exemplo:
 <h3>Quais opcionais você deseja?</h3>
 <input type="checkbox" name="opcional[]" value="queijo"> + queijo<br />
 <input type="checkbox" name="opcional[]" value="burger"> + burger<br />
 <input type="checkbox" name="opcional[]" value="tomate"> + tomate<br />
 
 Dessa forma eu estou explicitando que quando os valores forem enviados para o servidor, eu quero que no pedido x, sejam enviados todos os opcionais ajuntados; e assim por diante. Mas *atenção ao detalhe* de que eu incluo um array após opcional, no atributo name, justamente para que o servidor compreenda que estou me referindo a uma lista de valores de name="opcional"; Caso eu não inclua o colchetes, ele vai substituir cada valor pelo seguinte até registrar o último valor, que nesse caso seria value="tomate".
 
 > Radio: seleciona ou um ou outro. Mas isso precisa ser setado senão dá erro e seleciona mais de 1 (incorreto).
 
 A solução seria incluir um mesmo `name=""` para as opções dentre as quais o usuário deverá escolher, e diferenciar o valor de cada uma no atributo `value=""`. Assim, o programa saberá que o usuário deverá escolher apenas uma opção dentre as várias de mesma categoria. 
 
 <h3>Você deseja borda recheada de catupiry?</h3>
 <input type="radio" name="borda" value="sim"> sim<br />
 <input type="radio" name="borda" value="não"> não<br />
 
 ## Tag button e seus tipos (types)
 
 * Nessa tag conseguimos ter até 3 tipos de botões, os quais vão agir de forma semelhante mas com funcionalidades diferentes.
 
 Quando utilizamos o JS podemos adaptar todas as opções, mas em termos de HTML temos essas 3 principais.
 
 - `type="button" onclick="alert('cliquei')"` //Nesse caso incluímos uma função JS.

 - `type="reset"` // Limpa os buttons dentro do form no qual o button está incluído.

 - `type="submit" ` // Basicamente faz a submissão do formulário.

 > Em formulários, quando temos o `type="submit"` temos também o evento `onsubmit=""` que *é incluído dentro da tag geral do form em questão*, onde podemos incluir validações para a submissão. **Em outras palavras, esse evento é utilizado para validar o formulário antes de ser enviado ao servidor**.
 
 ## Select e seus tipos (types)

 * Atributo utilizado para determinar valores pré-definidos para serem exibidos em um determinado campo.
 
 > SELECT-BOX:
 
 Exemplo de uso:
 
 <body>
 	<form onsubmit="" method="get">
 		<label> Nome: </label><input type="text" name="nome"><br />
 		<label> Cargo: </label>
 		<select name="role">
 			<option value="">Selecione o cargo</option>
 			<option value="manager">Admin</option>
 			<option value="director">Diretoria</option>
 			<option value="lead">Líder</option>
 			
 > Nesse exemplo será apresentada uma aba com as opções para ser selecionada somente uma, e evitar que o usuário escreva literalmente qualquer coisa. É de acordo com os `values` que serão verificados os dados no servidor. 
 
 > Uma coisa interessante é que podemos usar `selected` para definir qual será o valor setado para aparecer na select box quando o formulário abrir.
 
 Por exemplo:
 <body>
 	<form onsubmit="" method="get">
 		<label> Nome: </label><input type="text" name="nome"><br />
 		<label> Cargo: </label>
 		<select name="role">
 			<option value="">Selecione o cargo</option>
 			<option selected value="manager">Admin</option>
 			<option value="director">Diretoria</option>
 			<option value="lead">Líder</option>
 			
 > TEXT-AREA:
 * Te permite criar um espaço específico para ser incluso mais texto do que nos outros campos. Ele tem um pre-set mas você pode estilizar ele de acordo com suas necessidades.
 
 <label>Mensagem:<label/>
 <textarea rows="" cols="" name="message"></textarea>
 
 
