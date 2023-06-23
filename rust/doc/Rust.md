# PRINCÍPIOS DO RUST

É uma linguagem moderna, de alto nível e de código aberto, desenvolvida com foco na segurança, desempenho e concorrência. Ela foi criada pela Mozilla Research e ganhou popularidade por sua abordagem inovadora para lidar com problemas comuns de programação, como bugs de memória, falhas de segurança e problemas de concorrência.

Uma das principais características do Rust é seu sistema de **tipos forte e estático**, que permite ao compilador detectar erros de tempo de compilação.

Ele usa um conceito chamado "emprestamento" (borrowing) para gerenciar a propriedade dos dados, o que significa que você precisa seguir certas regras ao passar dados entre diferentes partes do seu código, permitindo que você escreva código seguro e eficiente.

**Usando o Rust, muitas pessoas iniciantes podem aprender sobre conceitos de sistemas e uso de memória.**

# CONCEITOS COMUNS DA PROGRAMAÇÃO

## Variáveis e mutabilidade

Toda variável está associada a:

1. nome,
2. tipo,
3. valor,
4. endereço de memória RAM (&).

Cada tipo de dado possui um tamanho em Bit, que será alocado em variáveis e direcionados para endereços de memória RAM (cada qual com seu tamanho de acordo com o tipo de dado alocado).

Os endereços de memória declarados permanecem o mesmo, inalterados até o fim do programa. Essa região de memória fica bloqueada e corresponde à cada uma das variáveis.

**Referência**: https://www.youtube.com/watch?v=ucupombJuUM&ab_channel=xavecoding.

## Data types

Cada valor em Rust advém de um data type, que comunicará ao Rust o tipo de dado que está sendo especificado para que ele saiba como trabalhar com esse recurso.

Existem dois sub-conjuntos de data types: scalar and compound.

### Scalar (escalar)

É um tipo que representa um valor único.

Rust possui 5 scalar types primários;

1. Integer (inteiro)
2. booleanos (bool),
3. números inteiros [integer],
4. números de ponto flutuante [floating-point],
5. caracteres individuais (char)
6. ponteiros (raw pointers).

- **Integers (inteiro):**

| 8-bit   | i8    | u8    |
| ------- | ----- | ----- |
| 6-bit   | i32   | u32   |
| 32-bit  | i32   | u32   |
| 128-bit | i128  | u128  |
| arch    | isize | usize |

- Cada variante pode ser assinada (**signed**) ou não assinada (**unsigned**) e possui um tamanho explícito.

- Além disso, os tipos isize (signed) e usize (unsigned) dependem da arquitetura do computador (arch) em que seu programa está sendo executado, o que é indicado na tabela como "arch": 64 bits se você estiver em uma arquitetura de 64 bits e 32 bits se você estiver em uma arquitetura de 32 bits.

  **É importante escolher o tipo correto de acordo com os requisitos do seu programa para garantir a correta representação e manipulação dos valores inteiros.**

  _A diferença principal entre eles está na forma como interpretam e armazenam os valores._

**isize**: Os números inteiros assinados (isize) alocam um bit para representar o sinal (positivo ou negativo) e o restante dos bits para representar o valor absoluto. Isso significa que os números inteiros assinados têm uma faixa de valores negativos e positivos, mas a metade da faixa é usada para representar os números negativos.

**usize**: Os números inteiros não assinados (usize) não alocam um bit para representar o sinal, o que resulta em uma faixa maior de valores positivos. Isso significa que os números inteiros não assinados só podem representar valores positivos ou zero, sem a capacidade de armazenar números negativos.

- **Floating-point (número com casa decimal)**:

Existem dois tipos: f32 and f64, os quais são de tamanhos 32 8bits e 64 bits, respectivamente e oferecem diferentes níveis de precisão.

- O tipo f64 é default porque em CPUs modernos eles possuem basicamente a mesma velocidade que o f32 mas possui capacidade de maior precisão. Todos os pontos flutuantes são isize (signed).

- Os números de ponto flutuante seguem o padrão IEEE 754, que é um padrão amplamente utilizado para aritmética de ponto flutuante em computadores. Esse padrão define a forma como os números de ponto flutuante são representados, arredondados e operados.

- Os números de ponto flutuante em Rust podem ser expressos usando a notação decimal ou científica (exponencial). Por exemplo, 3.14 é um número de ponto flutuante válido em Rust, assim como 2.0e-3, que representa 2 multiplicado por 10 elevado à potência -3 (ou seja, 0.002).

* **Booleans (bool)**
  Representa um valor lógico amplamente utilizado em expressões condicionais para controlar fluxo de execução do programa (true : false) e possui tamanho de 1bit.

  **Exemplo:**

Em uma estrutura _condicional if_, a expressão dentro dos parênteses deve ser avaliada como um valor booleano. Se for true, o bloco de código associado ao if será executado. Caso contrário, o fluxo de execução pode passar para um bloco else ou continuar para a próxima instrução.

**Rust oferece os operadores lógicos para trabalhar com valores booleanos: && (E lógico), || (OU lógico) e ! (negação lógica).**

- **Characters (char)**
  O tipo char tem tamanho de 4bit e é sempre escrito dentro de single quote ( ‘ ‘ ) em oposição às strings que vão em double quotes ( “ “ ).

Representa um Valor Escalar Unicode, (unicode scalar value) o que significa que ele pode representar muito mais do que apenas ASCII. Letras acentuadas, caracteres chineses, japoneses e coreanos, emojis e espaços de largura zero são todos valores válidos do tipo char em Rust.

Referência do conteúdo específico de Rust: https://doc.rust-lang.org/book/ch03-03-how-functions-work.html.

## Coumpounds

Tipos compostos (compounds) podem agrupar múltiplos valores em um único tipo.

**Rust possui dois tipos compostos primitivos: tuplas e arrays.**

- **TUPLAS (tuple)**

Uma tupla é uma maneira geral de **agrupar um número de valores com diferentes tipos em um único tipo composto**.
As tuplas têm um tamanho fixo: uma vez declaradas, elas não podem crescer ou diminuir de tamanho.

Criamos uma tupla escrevendo uma lista separada por vírgulas de valores entre parênteses.

- Cada posição na tupla possui um tipo, e os tipos dos valores diferentes na tupla não precisam ser os mesmos.

Adicionamos anotações de tipo opcionais neste exemplo:

    fn main() {

    let tup: (i32, f64, u8) = (500, 6.4, 1);

    }

A variável "tup" se vincula à tupla porque um tuple é considerado um único elemento composto. Para obter os valores individuais de um tuple, podemos usar a correspondência de padrões para desestruturar um valor de tuple, como neste exemplo:

    fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;
       println!("The value of y is: {y}");
    }

Este programa primeiro cria uma tupla e a associa à variável "tup". Em seguida, utiliza um padrão com "let" para pegar a tupla e transformá-la em três variáveis separadas: x, y e z.
Isso é chamado de "destructuring" porque quebra a tupla única em três partes. Por fim, o programa imprime o valor de y, que é 6.4.

Também podemos acessar um elemento da tupla diretamente usando um ponto (.) seguido pelo índice do valor que desejamos acessar.
Por exemplo:

    fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
    }

Este programa cria a tupla x e, em seguida, acessa cada elemento da tupla usando seus respectivos índices.

**A tupla sem nenhum valor tem um nome especial, unit.**
Este valor e seu tipo correspondente são escritos como ( ) e representam um valor vazio ou um tipo de retorno vazio. _Expressões implicitamente retornam o valor unit se elas não retornam nenhum outro valor._

- **ARRAY**

Outra maneira de ter uma coleção de múltiplos valores é com um array. Ao contrário de uma tupla, cada elemento de um array deve ter o mesmo tipo. Ao contrário de arrays em algumas outras linguagens, arrays em Rust têm um tamanho fixo.

Escrevemos os valores em um array como uma lista separada por vírgulas dentro de colchetes:

     fn main() {
    	    let a = [1, 2, 3, 4, 5];
    }

Arrays são úteis quando você deseja alocar seus dados na pilha (stack) em vez do "heap" (discutiremos a pilha e o heap com mais detalhes no Capítulo 4) ou quando você deseja garantir que sempre tenha um número fixo de elementos. No entanto, **um array não é tão flexível quanto o tipo vetor.**

O vetor é um tipo de coleção semelhante fornecido pela biblioteca padrão que pode crescer ou diminuir de tamanho.

- **Os arrays são mais úteis quando você conhece o número de elementos que não precisarão ser alterados.**

Por exemplo, se você estivesse usando os nomes dos meses em um programa, provavelmente usaria um array em vez de um vector, porque sabe que ele sempre conterá 12 elementos:

    let months = ["January", "February", "March", "April", "May", "June",
     "July", "August", "September", "October", "November", "December"];

Você escreve o tipo de um array usando colchetes com o tipo de cada elemento, seguido de um ponto e vírgula e, em seguida, o número de elementos no array, como neste exemplo:

    let a: [i32; 5] = [1, 2, 3, 4, 5];

Aqui, i32 é o tipo de cada elemento. Após o ponto e vírgula, o número 5 indica que o array contém cinco elementos.

Você também pode inicializar um array para conter o mesmo valor para cada elemento, especificando o valor inicial, seguido por um ponto e vírgula e, em seguida, o tamanho do array entre colchetes, como mostrado aqui:

    let a = [3; 5];

O array chamado "a" conterá 5 elementos, que inicialmente serão todos definidos com o valor 3.
Isso é equivalente a escrever "let a = [3, 3, 3, 3, 3];", mas de forma mais concisa.

- **ACESSANDO ARRAYS**

Exemplo:

    fn main() {

    let a = [1, 2, 3, 4, 5];
    let first = a[0];
    let second = a[1];
    }

Se você rodar o código tentando bucar o índice "10", por exemplo, fora do escopo da quantidade de elementos no array, você receberá o seguinte erro no console:

    thread 'main' panicked at 'index out of bounds: the len is 5 but the index
     is 10', src/main.rs:19:19 note: run with `RUST_BACKTRACE=1`
     environment variable to display a backtrace.

O programa resultou em um erro em tempo de execução no momento em que foi usado um valor inválido na operação de indexação. O programa exibiu o erro e não executou a declaração final do println!.

Ao tentar acessar um elemento usando a indexação, o Rust verifica se o índice especificado é menor que o tamanho do array. Se o índice for maior ou igual ao tamanho, o Rust entrará em pânico. Essa verificação precisa ocorrer em tempo de execução, especialmente neste caso, porque o compilador não consegue saber qual valor o usuário irá inserir ao executar o código posteriormente.

**Isso é um exemplo dos princípios de segurança de memória do Rust em ação.**
_Em muitas linguagens de baixo nível, esse tipo de verificação não é feito e, quando você fornece um índice incorreto, é possível acessar memória inválida. O Rust protege você contra esse tipo de erro ao sair imediatamente em vez de permitir o acesso à memória e continuar a execução._

## FUNÇÕES

As funções são prevalentes no código Rust. Uma das funções mais importantes na linguagem é a `função main`, que é o ponto de entrada de muitos programas.

Utiliza-se snake_case como convenção para nomes de funções e variáveis.

Definimos uma função em Rust digitando fn seguido pelo nome da função e um conjunto de parênteses. As chaves delimitam o corpo da função, indicando onde ele começa e termina para o compilador.

    fn main() {
        println!("Hello, world!");
        another_function();
    }

    fn another_function() {
        println!("Another function.");
    }

Podemos chamar qualquer função que tenhamos definido digitando seu nome seguido de um conjunto de parênteses.

Como a função another_function está definida no programa, ela pode ser chamada de dentro da função main. Note que definimos another_function após a função main no código-fonte; também poderíamos tê-la definido antes.
O Rust não se importa onde você define suas funções, apenas que elas estejam definidas em algum lugar dentro de um escopo que possa ser visto pelo chamador.

As linhas são executadas na ordem em que aparecem na função main. Primeiro, a mensagem "Hello, world!" é impressa e, em seguida, another_function é chamada e sua mensagem é impressa "Another function".

## Parâmetros

Podemos incluir parâmetros nas funções, que **são variáveis especiais que fazem parte da assinatura de uma função**.

**Quando uma função tem parâmetros, você pode fornecer a ela valores concretos para esses parâmetros.**

Tecnicamente, os valores concretos são chamados de argumentos, mas, em conversas informais, **as pessoas tendem a usar as palavras parâmetro e argumento de forma intercambiável para as variáveis na definição de uma função ou para os valores concretos passados quando você chama uma função.**

A lista de parâmetros de uma função é chamada de assinatura. O nome e a assinatura de uma função a identificam de forma exclusiva.

**Como a própria palavra sugere, a assinatura da função é usada pelo compilador para distinguir entre as diferentes instâncias de funções sobrecarregadas.**

fn main() {
another_function(5);
}

    fn another_function(x: i32) {
        println!("The value of x is: {x}");
    }

    The value of x is: 5

A declaração da função another_function tem um parâmetro chamado x. O tipo de x é especificado como i32. Quando passamos 5 para another_function, a macro println! coloca o valor 5 onde estão os dois pares de chaves contendo x dentro da string.

**Nas assinaturas de funções, você deve declarar o tipo de cada parâmetro.**

Essa é uma decisão deliberada no design do Rust: exigir anotações de tipo nas definições de função significa que o compilador quase nunca precisa que você as use em outro lugar no código para descobrir qual tipo você quer dizer. O compilador também pode fornecer mensagens de erro mais úteis se ele souber quais tipos a função espera.

Ao definir vários parâmetros, separe as declarações dos parâmetros com vírgulas, assim como este exemplo:

    fn main() {
    print_labeled_measurement(5, 'h');
    }
    fn print_labeled_measurement(value: i32, unit_label: char) {

    println!("The measurement is: {value}{unit_label}");
    }

    The measurement is: 5h

Este exemplo cria uma função chamada print_labeled_measurement com dois parâmetros.

1. O primeiro parâmetro é chamado de value e é do tipo i32.
2. O segundo é chamado de unit_label e é do tipo char.
3. A função então imprime um texto contendo tanto o valor quanto o unit_label.

Neste exemplo, a função print_labeled_measurement recebe um value e um unit_label como argumentos.
Ela usa a macro println! para imprimir uma mensagem formatada que combina o valor e o rótulo da unidade.

- **STATEMENTS (declarações) AND EXPRESSIONS (expressões)**

Os corpos das funções são compostos por uma série de declarações, opcionalmente seguidas por uma expressão. Até agora, as funções que vimos não incluíam uma expressão final, mas você já viu uma expressão como parte de uma declaração.

Como o Rust é uma linguagem baseada em expressões, essa é uma distinção importante de se entender. Outras linguagens não possuem as mesmas distinções, então vamos ver o que são declarações e expressões e como suas diferenças afetam os corpos das funções.

Em Rust, uma declaração é uma instrução que realiza uma ação sem retornar um valor. Por exemplo, uma declaração pode ser a criação de uma variável, uma chamada de função ou um comando de controle de fluxo como um if ou um loop. As declarações são terminadas com um ponto e vírgula (;).

Uma expressão, por outro lado, avalia um valor e produz um resultado. As expressões podem ser utilizadas em declarações, como parte de uma atribuição ou como argumentos para uma chamada de função. Além disso, uma expressão também pode ser usada como a expressão final em um bloco de código, representando o valor retornado pela função.

Essa distinção é importante porque, em Rust, o valor de uma expressão final em uma função é automaticamente retornado, enquanto o valor de uma declaração não é. Isso significa que, se quisermos retornar um valor específico de uma função, devemos usar uma expressão como a última linha do corpo da função.

Em resumo, em Rust, declarações realizam ações sem retornar valores, enquanto expressões avaliam valores e podem ser usadas para retornar valores de uma função.

1.  **Statements**: são instruções que performam uma atividade mas não retornam nenhum valor.
    Creating a variable and assigning a value to it with the let keyword is a statement.
    For example: let y = 6; is a statement.

        fn main() {
        let y = 6;
        }

This is a main function declaration containing one statement.
**STATEMENTS DO NOT RETURN VALUES!**

Therefore, you can’t assign a let statement to another variable, as the following code tries to do; you’ll get an error: `This code does not compile!`
fn main() {
let x = (let y = 6);
}
The let y = 6 statement does not return a value, so there isn’t anything for x to bind to.

2.  **Expressions**: resultam em um valor.
    **EXPRESSIONS DO NOT INCLUDE SEMINOCOLON AT THE END.**

As expressões são avaliadas como um valor e constituem a maior parte do restante do código que você escreverá em Rust.

    fn main() {
    let y = {
    let x = 3;
    x + 1
    };
    println!("The value of y is: {y}");

}

This expression:

{
let x = 3;
x + 1
}

is a block that, in this case, evaluates to 4. That value gets bound to y as part of the let statement. Note that the x + 1 line doesn’t have a semicolon at the end, which is unlike most of the lines you’ve seen so far.

If you add a semicolon to the end of an expression, you turn it into a statement,
and it will then not return a value.
Keep this in mind!!!!!!

## FUNÇÕES COM VALORES NO RETURN

Funções podem retornar valores para o código que as chama.
**Não nomeamos os valores de retorno, mas devemos declarar seu tipo após uma seta (->).**

O valor de retorno da função é sinônimo do valor da expressão final no bloco do corpo da função.

**Você pode retornar antecipadamente de uma função usando a palavra-chave return e especificando um valor, mas na maioria das vezes as funções retornam implicitamente a última expressão.**

Aqui está um exemplo de uma função que retorna um valor:

    fn five() -> i32 {
    5
    }
    fn main() {
    let x = five();
    println!("The value of x is: {x}");
    }

Não há chamadas de função, macros ou mesmo declarações let na função five, apenas o número 5 por si só. Isso é perfeitamente válido em Rust.

Observe que o tipo de retorno da função também é especificado, como -> i32.

O 5 em five ( ) é o valor de retorno da função, por isso o tipo de retorno é i32.

Vamos examinar isso com mais detalhes.
Há duas partes importantes:

- Primeiro, a linha let x = five(); mostra que estamos usando o valor de retorno de uma função para inicializar uma variável. Como a função five retorna 5, aquela linha é equivalente a: `let x = 5;`

- Segundo, a função five não possui parâmetros e define o tipo do valor de retorno, mas o corpo da função é um solitário 5 sem ponto e vírgula porque é uma expressão cujo valor queremos retornar.

Vamos olhar para outro exemplo:

    fn plus_one(x: i32) -> i32 {
    x + 1
    }

    fn main() {
        let sominha = plus_one(9);
        println!("The value of sominha is: {sominha}");
    }

Executando este código, será impresso "O valor de sominha é: 10". **Mas se colocarmos um ponto-e-vírgula no final da linha contendo x + 1, transformando-a de uma expressão em uma declaração, receberemos um erro.**

A mensagem de erro principal, "mismatched types" (tipos incompatíveis), revela o problema central deste código.

A definição da `fn plus_one` diz que ela retornará um i32, mas declarações não avaliam um valor, o que é expresso por ( ), o tipo unit. Portanto, nada é retornado, o que contradiz a definição da função e resulta em um erro.

_Nessa saída, o Rust fornece uma mensagem para ajudar a corrigir esse problema: sugere remover o ponto-e-vírgula, o que resolveria o erro._

## CONTROL-FLOW (Controle de Fluxo)

Fala sobre a capacidade de executar algum código dependendo do fato de uma condição ser verdadeira e de executar algum código repetidamente enquanto uma condição for verdadeira.

**As construções mais comuns que permitem controlar o fluxo de execução do código Rust são as `expressões if e os loops`.**

- **if expressions**
  A estrutura de controle if (se) permite ramificar seu código dependendo de condições. Você fornece uma condição e, em seguida, diz: "Se essa condição for atendida, execute este bloco de código. Se a condição não for atendida, não execute este bloco de código."

      fn main() {
      let number = 3;

      if number < 5 {
      	println!("condition was true");
      	} else {
      println!("condition was false");
      	}
      }

Todas as `expressões if` começam com a palavra-chave if, seguida de uma condição. Neste caso, a condição verifica se a variável number tem um valor menor que 5. Colocamos o bloco de código a ser executado se a condição for verdadeira imediatamente após a condição, dentro de chaves.

Blocos de código associados às condições em expressões if são às vezes chamados de "arms".

Opcionalmente, **também podemos incluir uma expressão else**, o que fizemos aqui, _para fornecer ao programa um bloco de código alternativo a ser executado caso a condição seja avaliada como falsa_. Se você não fornecer uma expressão else e a condição for falsa, o programa simplesmente ignorará o bloco if e passará para a próxima parte do código.

**Também vale ressaltar que a condição neste código deve ser um bool.**

Se a condição não for um bool, ocorrerá um erro. Ao contrário de linguagens como Ruby e JavaScript, o Rust não tentará automaticamente converter tipos não booleanos em um booleano. Você deve ser explícito e sempre fornecer um valor booleano como condição para o if.

- **else if: lidando com múltiplas condições**

Podemos usar múltiplas condições combinando "if" e "else" em uma expressão "else if". Por exemplo:

    fn main() {
    let number = 6;
    if number % 4 == 0 {
    println!("number is divisible by 4");
    } else if number % 3 == 0 {
    println!("number is divisible by 3");
    } else if number % 2 == 0 {
    println!("number is divisible by 2");
    } else {
    println!("number is not divisible by 4, 3, or 2");
    }
    }

# Propriedade (ownership)

Algumas linguagens possuem coleta de lixo que regularmente busca por memória não mais utilizada enquanto o programa é executado; em outras linguagens, o programador deve explicitamente alocar e liberar a memória.

**Rust utiliza uma terceira abordagem: a memória é gerenciada através de um sistema de propriedade com um conjunto de regras que o compilador verifica.**

Se alguma das regras for violada, o programa não será compilado. Nenhuma das características da propriedade vai retardar o seu programa enquanto ele está sendo executado.

Por ser um conceito novo para muitos programadores, leva algum tempo para se acostumar com a propriedade. A boa notícia é que quanto mais experiência você adquirir com Rust e as regras do sistema de propriedade, mais fácil será para você desenvolver naturalmente um código seguro e eficiente.

## O Stack e o Heap

**O "stack" (pilha) e o "heap" (monte) são duas áreas de memória usadas em programas de computador.**

O **stack (pilha)** é uma região de memória organizada em uma estrutura de dados chamada de pilha. Ele é usado para armazenar informações sobre as chamadas de função, como endereços de retorno, parâmetros e variáveis locais.

A pilha é uma estrutura de dados de tamanho fixo e as operações de inserção e remoção são feitas de forma rápida, seguindo uma abordagem conhecida como LIFO (Last-In, First-Out, último a entrar, primeiro a sair). -> Pense na analogia de uma pilha de pratos, o primeiro a ser colocado na pilha será o último a ser retirado.

**All data stored on the stack must have a known, fixed size.**

O **heap (monte)**, por outro lado, é uma região de memória usada para alocação dinâmica. É onde os objetos ou dados são alocados quando o tamanho ou a vida útil não podem ser determinados antecipadamente. Diferentemente da pilha, o heap não segue uma organização estruturada fixa.

A alocação e liberação de memória no heap são mais flexíveis, mas também podem ser mais lentas do que as operações na pilha.

**AMBOS SÃO PARTES DA MEMÓRIA DISPONÍVEIS PARA O SEU CÓDIGO UTILIZAR EM TEMPO DE EXECUÇÃO (RUN TIME), PORÉM ESTÃO ESTRUTURADOS DE MANEIRAS DIFERENTES.**

O **heap** é menos organizado: quando você coloca dados no heap, você solicita uma determinada quantidade de espaço. O alocador de memória encontra um local vazio no heap que seja grande o suficiente, marca-o como em uso e retorna um ponteiro, que é o endereço desse local. Esse processo é chamado de alocação no heap e às vezes é abreviado apenas como alocação (colocar valores na pilha não é considerado alocação).

Como o ponteiro para o heap tem um tamanho conhecido e fixo, você pode armazenar o ponteiro na pilha, mas quando você deseja os dados reais, você deve seguir o ponteiro.

Pense em estar sentado em um restaurante. Quando você entra, você informa o número de pessoas do seu grupo, e o anfitrião encontra uma mesa vazia que acomode todos e o leva até lá. Se alguém do seu grupo chegar tarde, eles podem perguntar onde vocês estão sentados para encontrá-los.

**Acessar dados no heap é mais lento do que acessar dados na pilha, porque é necessário seguir um ponteiro para chegar lá.**

_Os processadores contemporâneos são mais rápidos se pularem menos pela memória._

Continuando com a analogia, imagine um servidor em um restaurante recebendo pedidos de várias mesas. É mais eficiente pegar todos os pedidos de uma mesa antes de passar para a próxima mesa. Pegar um pedido da mesa A, depois um pedido da mesa B, e então um pedido da mesa A novamente, seguido de um pedido da mesa B novamente seria um processo muito mais lento.

Da mesma forma, um processador pode executar seu trabalho melhor se trabalhar em dados que estão próximos a outros dados (como na stack), em vez de estarem mais distantes (como pode ocorrer no heap).

**Manter o controle de quais partes do código estão usando quais dados na memória heap, minimizando a quantidade de dados duplicados na heap e limpando os dados não utilizados na heap para evitar falta de espaço são todos problemas que a propriedade aborda.** Uma vez que você compreenda a propriedade, você não precisará pensar frequentemente sobre a pilha e a heap, mas saber que o principal objetivo da propriedade é gerenciar dados na heap pode ajudar a explicar por que ela funciona da maneira que funciona.

- **Ownership rules (regras da propriedade)**

1.  Cada valor em Rust possui um proprietário.
2.  Só pode haver um único proprietário por vez.
3.  Quando o proprietário sai do escopo, o valor será descartado.

## Escopo de variável

Como primeiro exemplo de propriedade, vamos analisar o escopo de algumas variáveis. Um escopo é o intervalo dentro de um programa no qual um item é válido.

```rust
 {                      // s is not valid here, it’s not yet declared
        let s = "hello";   // s is valid from this point forward

        // do stuff with s
    }                      // this scope is now over, and s is no longer valid
```

## Data type String

Os tipos abordados até então têm um tamanho conhecido, podem ser armazenados na pilha (stack) e removidos da pilha quando seu escopo termina, podendo também ser rapidamente e facilmente copiados para criar uma nova instância independente, caso outra parte do código precise usar o mesmo valor em um escopo diferente.

As string literais (tipo primitivo) são convenientes, mas não são adequadas para todas as situações em que podemos querer usar texto porque elas são imutáveis. Outra razão é que nem todo valor de string pode ser conhecido quando escrevemos nosso código: por exemplo, e se quisermos receber entrada do usuário e armazená-la?

Para essas situações, o Rust possui um segundo tipo de string, String. Esse tipo gerencia dados alocados no heap e, como tal, é capaz de armazenar uma quantidade de texto desconhecida para nós durante o tempo de compilação. Você pode criar uma String a partir de uma literal de string usando a função from, assim:

```rust
    let mut s = String::from("hello");

    s.push_str(", world!"); // push_str() appends a literal to a String

    println!("{}", s); // This will print `hello, world!`
```

**Por que String é mutável e o tipo primitivo string literal não pode?** _Porque a diferença está em como esses dois tipos de dados lidam com memória._

## Memória e Alocação

Por conta da imutabilidade da string literal, nós podemos saber o seu conteúdo no tempo de compilação, uma vez que o texto dela está codificado diretamente na execução final.

Com o tipo String, a fim de suportar um texto mutável e expansível, precisamos alocar uma quantidade de memória no heap (monte), desconhecida em tempo de compilação, para armazenar o conteúdo.

- A memória deve ser solicitada ao alocador de memória em tempo de execução.
- Precisamos de um meio de devolver essa memória ao alocador quando terminarmos de usar nossa String.

**A primeira parte é feita por nós:** quando chamamos String::from, sua implementação solicita a memória necessária. Isso é praticamente universal em linguagens de programação.

No entanto, **a segunda parte é diferente**.

Em linguagens com um coletor de lixo (GC), o GC controla e limpa a memória que não está mais sendo usada, e não precisamos pensar nisso. Na maioria das linguagens sem um GC, é nossa responsabilidade identificar quando a memória não está mais sendo usada e chamar código para liberá-la explicitamente, assim como fizemos para solicitá-la. Fazer isso é difícil.

Se esquecermos, iremos desperdiçar memória. Se fizermos isso muito cedo, teremos uma variável inválida. Se fizermos duas vezes, isso também é um bug. **_Precisamos combinar exatamente uma alocação com exatamente uma liberação._**

**Em Rust, a memória é devolvida automaticamente assim que a variável que a possui sai de escopo.** Aqui está uma versão do nosso exemplo de escopo do Exemplo 4-1 usando uma String em vez de uma string literal:

```rust
{
        let s = String::from("hello"); // s is valid from this point forward

        // do stuff with s
    }                                  // this scope is now over, and s is no
                                       // longer valid
```

**This pattern has a profound impact on the way Rust code is written. It may seem simple right now, but the behavior of code can be unexpected in more complicated situations when we want to have multiple variables use the data we’ve allocated on the heap. Let’s explore some of those situations now.**

- **Variáveis e Interação de Dados com o Movimento**
  Multiple variables can interact with the same data in different ways in Rust. Exemplo:

```rust
 let x = 5;
 let y = x;
```

Podemos deduzir que está acontecendo: "atribuir o valor 5 a x; em seguida, fazer uma cópia do valor em x e atribuí-lo a y." Agora temos duas variáveis, x e y, e ambas são iguais a 5. _Isso é realmente o que está acontecendo, porque os inteiros são valores simples com um tamanho conhecido e fixo, e esses dois valores 5 são colocados na pilha_.

Agora, nesse próximo caso, podemos assumir que ocorreria o mesmo:

```rust
let s1 = String::from("hello");
    let s2 = s1;

```

Uma String é composta por três partes, conforme ilustra a coluna da esquerda: um ponteiro para a memória que armazena o conteúdo da string, um comprimento e uma capacidade. Esse grupo de dados é armazenado na pilha.
À direita está a memória no heap que armazena o conteúdo.
![Figure 4-1: Representation in memory of a `String` holding the value `"hello"` bound to `s1`](https://doc.rust-lang.org/book/img/trpl04-01.svg)

**Lenght** (comprimento) é a quantidade de memória, em bytes, que o conteúdo da String está usando atualmente. A **capacidade** é a quantidade total de memória, em bytes, que a String recebeu do alocador. _A diferença entre o comprimento e a capacidade é importante, mas não neste contexto, então por enquanto, é seguro ignorar a capacidade._

Quando atribuímos s1 a s2, os dados da String são copiados, o que significa que copiamos o ponteiro, o comprimento e a capacidade que estão na pilha. Não copiamos os dados no heap para onde o ponteiro se refere. Em outras palavras, a representação dos dados na memória é semelhante à:

![Figure 4-2: Representation in memory of the variable `s2` that has a copy of the pointer, length, and capacity of `s1`](https://doc.rust-lang.org/book/img/trpl04-02.svg)

![Figure 4-3: Another possibility for what `s2 = s1` might do if Rust copied the heap data as well](https://doc.rust-lang.org/book/img/trpl04-03.svg)

Já foi dito que quando uma variável sai de escopo, o Rust chama automaticamente a função `drop` e limpa a memória alocada no heap para aquela variável.

Mas a Figura 4-2 mostra ambos os ponteiros de dados apontando para o mesmo local. Isso é um problema: quando s2 e s1 saem de escopo, ambas tentarão liberar a mesma memória. Isso é conhecido como um erro de "double free" e é um dos bugs de segurança de memória que mencionamos anteriormente. Liberar a memória duas vezes pode levar à corrupção de memória, o que potencialmente pode resultar em vulnerabilidades de segurança.

Para garantir a segurança da memória, após a linha `let s2 = s1;`, o Rust considera s1 como inválido.

Se você já ouviu os termos "cópia rasa" (shallow copy) e "cópia profunda" (deep copy) ao trabalhar com outras linguagens, o conceito de copiar o ponteiro, o tamanho e a capacidade sem copiar os dados provavelmente parece ser uma cópia rasa.

**Mas porque o Rust também invalida a primeira variável, em vez de ser chamado de uma cópia rasa, é conhecido como uma movimentação (move).** Neste exemplo, diríamos que s1 foi movido para s2. Então, o que realmente acontece é mostrado na Figura 4-4.

![enter image description here](https://doc.rust-lang.org/book/img/trpl04-04.svg)

Isso resolve nosso problema! Com apenas s2 válido, quando ele sair de escopo, ele sozinho liberará a memória e estaremos prontos.

Além disso, há uma escolha de design implícita nisso: o Rust nunca criará automaticamente cópias "profundas" dos seus dados. Portanto, qualquer cópia automática pode ser considerada rasa em termos de desempenho em tempo de execução.

- **Variables and Data Interacting with Clone**
  Se quisermos copiar profundamente os dados do heap da String, não apenas os dados da pilha (stack), podemos usar um método comum chamado `clone`. Discutiremos a sintaxe dos métodos no Capítulo 5, mas como os métodos são uma característica comum em muitas linguagens de programação, você provavelmente já os viu antes.

Aqui está um exemplo do método clone em ação:

```rust
   let s1 = String::from("hello");
    let s2 = s1.clone();

    println!("s1 = {}, s2 = {}", s1, s2);
```

Isso funciona muito bem e produz explicitamente o comportamento mostrado na Figura 4-3, onde os dados do heap são copiados.

- **Stack-Only Data: Copy**

Rust possui uma anotação especial chamada de trait Copy que podemos colocar em tipos armazenados na pilha, como os inteiros (falaremos mais sobre traits no Capítulo 10). Se um tipo implementa o trait Copy, as variáveis que o utilizam não são movidas, mas sim copiadas trivialmente, tornando-as válidas mesmo após serem atribuídas a outra variável.

Rust não permite que anotemos um tipo com Copy se o tipo, ou qualquer uma de suas partes, implementou o trait Drop (saiu do escopo). Se o tipo precisa de algo especial para acontecer quando o valor sai de escopo e adicionamos a anotação Copy a esse tipo, receberemos um erro de compilação.

**Então, quais tipos implementam o trait Copy?**
Você pode verificar a documentação do tipo específico para ter certeza, mas como regra geral, **qualquer grupo de valores escalares simples pode implementar Copy, e nada que exija alocação ou seja uma forma de recurso pode implementar Copy.** Aqui estão alguns dos tipos que implementam Copy:

- Todos os tipos de inteiros, como u32.
- O tipo booleano, bool, com os valores true e false.
- Todos os tipos de ponto flutuante, como f64.
- O tipo de caractere, char.
- Tuplas, se contiverem apenas tipos que também implementam Copy. _Por exemplo, (i32, i32) implementa Copy, mas (i32, String) não._

* **Ownership and Functions**

A mecânica de passar um valor para uma função é similar àquela de atribuir um valor a uma variável. Passar uma variável para uma função irá mover ou copiar, assim como a atribuição faz.

```rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it's okay to still
                                    // use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{}", some_string);
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{}", some_integer);
} // Here, some_integer goes out of scope. Nothing special happens.
```

Se tentássemos usar `s` após a chamada para `takes_ownership`, o Rust lançaria um erro de compilação. Essas verificações estáticas nos protegem de erros. Tente adicionar código ao `main` que usa `s` e `x` para ver onde você pode usá-los e onde as regras de propriedade impedem que você faça isso.

- **Return Values and Scope**
  Retornar valores também pode transferir a propriedade. O próximo exemplo mostra uma função que retorna algum valor, com anotações similares às do exemplo anterior.

```rust
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1

    let s2 = String::from("hello");     // s2 comes into scope

    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

    a_string  // a_string is returned and moves out to the calling function
}
```

A propriedade de uma variável segue o mesmo padrão sempre: atribuir um valor a outra variável o faz se mover Quando uma variável que inclui dados no heap sai do escopo, o valor será limpo pelo "drop" a menos que a propriedade dos dados tenha sido movida para outra variável.

Embora isso funcione, assumir a propriedade e em seguida retornar a propriedade com cada função é um pouco tedioso.
E se quisermos permitir que uma função use um valor sem assumir a propriedade?

É bastante irritante que qualquer coisa que passamos também precise ser retornada se quisermos usá-la novamente, além de qualquer dado resultante do corpo da função que também possamos querer retornar.

**Rust does let us return multiple values using a tuple, as shown next.**

```rust
fn main() {
    let s1 = String::from("hello");

    let (s2, len) = calculate_length(s1);

    println!("The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() returns the length of a String

    (s, length)
}
```
