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
