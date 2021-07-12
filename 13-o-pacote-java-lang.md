# O Pacote java.lang
_"Nossas cabeças são redondas para que os pensamentos possam mudar de direção." -- Francis
Piacaba_

Ao final deste capítulo, você será capaz de:

* Utilizar as principais classes do pacote `java.lang` e ler a documentação padrão de projetos
Java;
* Usar a classe `System` para obter informações do sistema;
* Fazer uso da classe `String` de uma maneira eficiente e conhecer seus detalhes;
* Utilizar os métodos herdados de `Object` para generalizar seu conceito de objetos.




## Pacote java.lang

Já usamos, por diversas vezes, as classes `String` e `System`. Vimos o sistema de pacotes do
Java e nunca precisamos dar um `import` nessas classes. Isso ocorre porque elas estão dentro do
pacote `java.lang`, que é **automaticamente importado** para você. É o **único pacote** com essa
característica.

Vejamos um pouco de suas principais classes.

## Um pouco sobre a classe System
A classe `System` possui uma série de atributos e métodos estáticos. Já usamos o
atributo `System.out` para imprimir.

Olhando a documentação, você compreenderá que o atributo `out` é do tipo `PrintStream`
do pacote `java.io`. Veremos sobre essa classe mais adiante. Já podemos
perceber que poderíamos quebrar o `System.out.println` em duas linhas:

``` java
PrintStream saida = System.out;
saida.println("ola mundo!");
```

 



O `System` conta também com um método que simplesmente desliga a Java Virtual Machine e retorna um
código de erro para o sistema operacional. Esse método é o `exit`.

``` java
	System.exit(0);
```

Veremos também um pouco mais sobre a classe `System` nos próximos capítulos e no apêndice de `Threads`.
Consulte a documentação do Java e veja outros métodos úteis da `System`.

## java.lang.Object
Em todo método no qual precisamos receber algum parâmetro, temos de declarar o seu tipo. Por exemplo, no nosso método `saca`, precisamos passar como parâmetro um valor do tipo `double`. Se tentarmos passar qualquer coisa diferente disso, teremos um erro de compilação.

Agora observemos o seguinte método do próprio Java:

``` java
System.out.println("Olá mundo!");
```

Nesse caso, o método `println` está recebendo uma `String`, e poderíamos pensar que o tipo de parâmetro que ele recebe é `String`. Mas, ao mesmo tempo, podemos passar para esse método coisas completamente diferentes como `int`, `Conta`, `Funcionario`, `SeguroDeVida`, etc. Como ele consegue receber tantos parâmetros de tipos diferentes?

Uma possibilidade seria o uso da sobrecarga, declarando um `println` para cada tipo de objeto diferente. Mas claramente não é isso que acontece, posto que conseguiríamos criar uma classe qualquer, invocar o método `println`, passar essa nova classe como parâmetro, e ele funcionaria!

Para entender o que está acontecendo, consideraremos um método que recebe uma `Conta`:

``` java
public void imprimeDados(Conta conta) {
	System.out.println(conta.getTitular() + " - " + conta.getSaldo());
}
```

Esse método pode ser invocado passando como parâmetro qualquer tipo de conta que temos no nosso sistema: `ContaCorrente` e `ContaPoupanca`, pois ambas são filhas de `Conta`. Se quiséssemos que o nosso método conseguisse receber qualquer tipo de objeto, teríamos de ter uma classe a qual fosse mãe de todos esses objetos. É para isso que existe a classe `Object`!

Sempre quando declaramos uma classe, esta é **obrigada** a herdar de outra. Isto é, para toda
classe que declararmos, existe uma superclasse. Porém, criamos diversas classes sem herdar de
ninguém:

``` java
	class MinhaClasse {

	}
```


Quando o Java não encontra a palavra-chave `extends`, ele considera que você está herdando da
classe `Object`, que também se encontra dentro do pacote `java.lang`. Você até mesmo pode
escrever essa herança, que é o mesmo:

``` java
	public class MinhaClasse extends Object {

	}
```

**Todas as classes, sem exceção, herdam de `Object`**, seja direta ou indiretamente, pois
ela é a mãe, vó, bisavó, etc. de qualquer classe.

Podemos também afirmar que qualquer objeto em Java é um `Object` e pode ser referenciado como
tal. Então qualquer objeto tem todos os métodos declarados na classe `Object`, e veremos alguns
deles logo após o _casting_.



## Métodos do java.lang.Object: equals e toString

### toString


A habilidade de poder se referir a qualquer objeto como `Object` nos oferece muitas vantagens. Podemos
criar um método que recebe um `Object` como argumento, isto é, qualquer objeto! Por exemplo, o método `println` poderia ser implementado da seguinte maneira:

``` java
public void println(Object obj) {
	write(obj.toString()); // o método write escreve uma string no console
}
```

Dessa forma, qualquer objeto que passarmos como parâmetro poderá ser impresso no console, desde que ele tenha o método `toString`. Para garantir que todos os objetos do Java tenham esse método, ele foi implementado na classe `Object`.

Por padrão, o método `toString` do `Object` retorna, concatenados: o nome da classe, `@` e um número de identidade. Vejamos um exemplo abaixo:

```
Conta@34f5d74a
```

Mas e se quisermos imprimir algo diferente? Na nossa tela de detalhes de conta, temos uma caixa de seleção na qual nossas contas estão sendo apresentadas com o valor do padrão do `toString`. Sempre que queremos modificar o comportamento de um método em relação à implementação herdada da superclasse, podemos sobrescrevê-lo na classe filha:

``` java
public abstract class Conta {
    protected double saldo;
    // outros atributos...
	
    @Override
    public String toString() {
        return "[titular=" + titular + ", numero=" + numero
            + ", agencia=" + agencia + "]";
    }	
}
```

Agora podemos usar esse método assim:

``` java
	ContaCorrente cc = new ContaCorrente();
	System.out.println(cc.toString());
```

 

E o melhor: se for apenas para jogar na tela, nem precisa chamar o `toString`! Ele já é
chamado para você:

``` java
	ContaCorrente cc = new ContaCorrente();
	System.out.println(cc); // O toString é chamado pela classe PrintStream
```

 

Gera o mesmo resultado!

Você ainda pode concatenar `Strings` em Java com o operador `+`. Se o Java encontra um objeto no
meio da concatenação, ele também chama o seu `toString`.

``` java
	ContaCorrente cc = new ContaCorrente();
	System.out.println("Conta: " + cc);
```

### equals

Até agora estamos ignorando o fato que podemos ter mais de uma conta de mesmo número e agência no nosso sistema. Atualmente, quando inserimos uma nova conta, o sistema verifica se a conta inserida é igual a alguma outra conta já cadastrada. Mas qual critério de igualdade é utilizado por padrão para fazer essa verificação?

Assim como no caso do `toString`, todos objetos do Java têm um outro método chamado `equals`, que é utilizado para comparar objetos daquele tipo. Por padrão, esse método apenas compara as referências dos objetos. Como toda vez que inserimos uma nova conta no sistema estamos fazendo `new` em algum tipo de conta, as referências nunca vão ser iguais, mesmo que os dados (número e agência) tenham os mesmos valores de uma conta para outra.


Mas e se fosse preciso comparar os atributos? Quais atributos ele deveria comparar? O Java por si
só não faz isso, mas podemos sobrescrever o `equals` da classe `Object` para criarmos esse
critério de comparação.

O `equals` recebe um `Object` como argumento e deve verificar se ele mesmo é igual ao `Object`
recebido para retornar um `boolean`. Se você não reescrever esse método, o comportamento herdado é
fazer um `==` com o objeto recebido como argumento.

``` java
	public abstract class Conta {
		protected double saldo;
		// outros atributos...
	
		public boolean equals(Object object) {
			// primeiro verifica se o outro object não é nulo
			if (object == null) {
				return false;
			}

			if (this.numero == object.numero &&
				this.agencia.equals(object.agencia)) {
				return true;
			}
			return false;
		}
	}
```

### Casting de referências

No momento em que recebemos uma referência a um `Object`, como acessaremos os métodos e atributos desse objeto que imaginamos ser uma `Conta` se estamos referenciando-o como `Object`? Não podemos acessá-lo sendo
`Conta`. O código acima não compila!

Poderíamos, então, atribuir essa referência de `Object` a `Conta` para depois
acessarmos os atributos necessários? Tentemos:

``` java
Conta outraConta = object;
```

Nós temos certeza de que esse `Object` se refere a uma `Conta`, uma vez que a nossa lista só imprime contas. Mas o compilador Java não tem garantia disso!
Essa linha acima não compila, pois nem todo `Object` é uma `Conta`.


A fim de realizar essa atribuição, devemos avisar o compilador Java que realmente queremos
fazer isso, sabendo do risco que corremos. Façamos o **casting de referências** parecido com o
de tipos primitivos:

``` java
Conta outraConta = (Conta) object;
```

O código passa a compilar, mas será que roda? Esse código roda sem nenhum problema, pois, em
tempo de execução, a JVM verificará se essa referência realmente é a um objeto de tipo `Conta`! Se não fosse, uma exceção do tipo `ClassCastException` seria lançada.

Com isso, nosso método `equals` ficaria assim:

``` java
	public abstract class Conta {
		protected double saldo;
		// outros atributos...
	
		public boolean equals(Object object) {
			if (object == null) {
				return false;
			}

			Conta outraConta = (Conta) object;
			if (this.numero == outraConta.numero &&
				this.agencia.equals(outraConta.agencia)) {
				return true;
			}
			return false;
		}
	}
```

Você poderia criar um método com outro nome em vez de reescrever `equals`, que recebe `Object`. Mas
o `equals` é importante, pois muitas bibliotecas o chamam mediante ao polimorfismo, como veremos no capítulo
do `java.util`.

O método `hashCode()` anda de mãos dadas com o método `equals()` e é de fundamental entendimento
no caso de você utilizar suas classes com estruturas de dados que usam tabelas de espalhamento.
Também falaremos dele no capítulo de `java.util`.

> **Regras para a reescrita do método equals**
>
> Pelo contrato definido pela classe `Object`, devemos retornar `false` também, contanto que o objeto
> passado não seja de tipo compatível com a sua classe. Então, antes de fazer o casting, devemos verificar
> isso e, para tal, usamos a palavra-chave `instanceof`, ou teríamos uma exception sendo lançada.
>
> Além disso, podemos resumir nosso `equals` de tal forma a não usar um `if`:
>
> ``` java
> 		public boolean equals(Object object) {
> 			if (object == null) {
> 				return false;
> 			}
> 			if (!(object instanceof Conta)) {
> 				return false;
> 			}
> 			Conta outraConta = (Conta) object;
> 			return (this.numero == outraConta.numero &&
> 				this.agencia.equals(outraConta.agencia));
> 		}
> ```




## Exercícios: java.lang.Object
1. Como verificar se a classe `Throwable`, que é a superclasse de `Exception`, também reescreve o método `toString`?

	A maioria das classes do Java que são muito utilizadas terão seus métodos
	`equals` e `toString` reescritos convenientemente.

	
1. Utilize-se da documentação do Java e descubra de que classe é o objeto
	referenciado pelo atributo `out` da `System`.

	Repare que, com o devido `import`, poderíamos escrever:

	``` java
	// falta a declaração da saída
	________ saida = System.out;
	saida.println("ola");
	```

	Por qual tipo a variável `saida` precisa ser declarada? É isso
	que você precisa descobrir. Se você digitar esse código no Eclipse, ele
	irá sugerir a você um quickfix e lhe declarará a variável.

	Estudaremos essa classe em um capítulo futuro.

	
1. Rode a aplicação e cadastre duas contas. Na tela de detalhes de conta, verifique o que aparece na caixa de seleção de conta para transferência.
	Por que isso acontece?

	
1. Reescreva o método `toString` da sua classe `Conta` fazendo com que uma
	mensagem mais explicativa seja devolvida. Lembre-se de aproveitar os recursos
	do Eclipse para isso: digitando apenas o começo do nome do método a ser reescrito
	e pressionando **Ctrl + espaço**, ele sugerirá reescrever o método, poupando-o
	do trabalho de escrever a assinatura dele e de cometer algum engano.

	``` java
	public abstract class Conta {

      protected double saldo;

	    @Override
	    public String toString() {
	        return "[titular=" + titular + ", numero=" + numero
               + ", agencia=" + agencia + "]";
	    }
      // restante da classe

	}
	```

	Rode a aplicação novamente, cadastre duas contas e verifique, outra vez, a caixa de seleção da transferência. O que aconteceu?

	
1. Reescreva o método `equals` da classe `Conta` para que duas contas com o
	mesmo **número e agência** sejam consideradas iguais. Esboço:

	``` java
	public abstract class Conta {

		public boolean equals(Object obj) {
			if (obj == null) {
				return false;
			}

			Conta outraConta = (Conta) obj;

			return this.numero == outraConta.numero && 
				this.agencia.equals(outraConta.agencia);
		}
	}
	```

	

	Você pode usar o **Ctrl + espaço** do Eclipse para escrever o esqueleto do
	método `equals`. Basta digitar dentro da classe `equ` e pressionar
	**Ctrl + espaço**.

	Rode a aplicação e tente adicionar duas contas com o mesmo número e agência. O que acontece?


## java.lang.String

`String` é uma classe em Java. Variáveis do tipo `String` guardam referências a objetos, e não
um valor, como acontece com os tipos primitivos.

Aliás, podemos criar uma `String` utilizando o `new`:

``` java
	String x = new String("fj11");
	String y = new String("fj11");
```

Criamos aqui dois objetos diferentes. O que acontece quando comparamos essas duas referências
utilizando o `==`?

``` java
	if (x == y) {
		System.out.println("referência para o mesmo objeto");
	}
	else {
		System.out.println("referências para objetos diferentes!");
	}
```

 

Temos aqui dois objetos distintos! E, então, como faríamos para verificar se o conteúdo do objeto é
o mesmo? Utilizamos o método `equals`, que foi reescrito pela `String`, com o objetivo de fazer a comparação
de `char` em `char`.

``` java
	if (x.equals(y)) {
		System.out.println("consideramos iguais no critério de igualdade");
	}
	else {
		System.out.println("consideramos diferentes no critério de igualdade");
	}
```

 

Aqui, a comparação retorna verdadeiro. Por quê? Pois quem implementou a classe `String` decidiu que
esse seria o melhor critério de comparação. Você pode descobrir os critérios de igualdade de cada
classe pela documentação.

Podemos também concatenar `Strings` usando o `+`, além de concatenar `Strings` com qualquer
objeto e até mesmo números:

``` java
	int total = 5;
	System.out.println("o total gasto é: " + total);
```

O compilador utilizará os métodos apropriados da classe `String` e possivelmente métodos de outras
 classes para realizar tal tarefa.


Se quisermos comparar duas Strings, utilizamos o método `compareTo`, que recebe uma `String` como
argumento e devolve um inteiro indicando se a `String` vem antes, é igual ou vem depois da
`String` recebida. Se forem iguais, é devolvido `0`; se for anterior à `String` do argumento,
um inteiro negativo; e, se for posterior, um inteiro positivo.

Fato importante: **uma String é imutável**. O Java cria um _pool_ de Strings para usá-lo como _cache_. Se
a `String` não fosse imutável, mudando o valor de uma `String`, afetaria todas as `String`s de outras
classes que tivessem o mesmo valor.

Repare no código abaixo:

``` java
	String palavra = "fj11";
	palavra.toUpperCase();
	System.out.println(palavra);
```

 

Pode parecer estranho, mas ele imprime "fj11" em minúsculo. Todo método que parece alterar o valor
de uma `String`, na verdade, cria uma nova `String` com as mudanças solicitadas e a retorna! Tanto
que esse método não é `void`. O código realmente útil ficaria assim:

``` java
	String palavra = "fj11";
	String outra = palavra.toUpperCase();
	System.out.println(outra);
```

 

Ou você pode eliminar a criação de outra variável temporária se achar conveniente:

``` java
	String palavra = "fj11";
	palavra = palavra.toUpperCase();
	System.out.println(palavra);
```

Isso funciona da mesma forma para **todos** os métodos que parecem alterar o conteúdo de uma `String`.

Se você ainda quiser trocar o número 1 para 2, faríamos:

``` java
	String palavra = "fj11";
	palavra = palavra.toUpperCase();
	palavra = palavra.replace("1", "2");
	System.out.println(palavra);
```

Ou ainda poderíamos concatenar as invocações de método, já que uma `String` é devolvida a cada invocação:

``` java
	String palavra = "fj11";
	palavra = palavra.toUpperCase().replace("1", "2");
	System.out.println(palavra);
```

O funcionamento do pool interno de Strings do Java tem uma série de detalhes, e você pode encontrar
mais informações sobre isso na documentação da classe `String` e no seu método
`intern()`.

> **Outros métodos da classe `String`**
>
> Existem diversos métodos da classe `String` que são extremamente importantes. Recomendamos sempre
> consultar o Javadoc relativo a essa classe para aprender cada vez mais sobre ela.
>
> Por exemplo, o método `charAt(i)` retorna o caractere existente na posição `i` da String. O
> **método** `length()` retorna o número de caracteres na mesma posição, e o método `substring(i)` recebe um
> `int` e devolve a subString a partir da posição passada por esse `int`.
>
> O `indexOf` recebe um char ou uma String e devolve o índice em que aparece, pela primeira vez, na String
> principal (há também o `lastIndexOf` que devolve o índice da última ocorrência).
>
> O `toUpperCase` e o `toLowerCase` devolvem uma nova String toda em maiúscula e toda em minúscula,
> respectivamente.
>
> A partir do Java 6, temos ainda o método `isEmpty`, que devolve `true` se a String for vazia, ou
> `false`, caso contrário.
>
> Alguns métodos úteis para buscas são o `contains` e o `matches`.
>
> Há muitos outros métodos. Recomendamos que você sempre consulte o Javadoc da classe.




> **java.lang `StringBuffer` e `StringBuilder`**
>
> Como a classe `String` é imutável, trabalhar com uma mesma `String` diversas vezes pode ter um efeito colateral:
> gerar inúmeras `String`s temporárias. Isso prejudica a performance da aplicação consideravelmente.
>
> Se porventura você trabalhar muito com a manipulação de uma mesma `String` (por exemplo, dentro de um laço), o
> ideal é utilizar a classe `StringBuffer`, pois esta representa uma sequência de caracteres.
> Diferentemente da `String`, ela é mutável e não tem aquele pool.
>
> A classe `StringBuilder` tem exatamente os mesmos métodos, com a diferença de ela não ser **thread-safe**. Esse conceito está descrito no
> capítulo apêndice de Threads.String.




## Exercícios: java.lang.String
1. Queremos que as contas apresentadas na caixa de seleção da transferência apareçam com o nome do titular em maiúsculas. A fim de fazê-lo, alteraremos o método `toString` da classe `Conta`. Utilize o método `toUpperCase` da `String` para isso.

	
1. Após alterarmos o método `toString`, aconteceu alguma mudança com o nome do titular que é apresentado na lista de contas? Por quê?

	
1. Teste os exemplos desse capítulo para ver que uma `String` é imutável.
	Por exemplo:

	``` java
		public class TestaString {

			public static void main(String[] args) {
				String s = "fj11";
				s.replaceAll("1", "2");
				System.out.println(s);
			}

		}
	```

	Como fazê-lo imprimir "fj22"?

	
1. Como sabemos se uma `String` se encontra dentro de outra?
	Como fazemos para tirar os espaços em branco das pontas de uma `String`? Como sabemos
	se uma `String` está vazia? Quantos caracteres
	tem uma `String`?

	Tome como hábito sempre pesquisar o Javadoc! Conhecer a API, aos
	poucos, é fundamental para que você não precise reescrever a roda!
	
1. (Opcional) Escreva um método que usa os métodos `charAt` e `length` de uma
	`String` para imprimí-la caractere caractere, com
	cada caractere em uma linha diferente.

	
1. (Opcional) Reescreva o método do exercício anterior, mas modificando-o para que
	imprima a `String` de trás para a frente e em uma linha só. Teste-a para
	_"Socorram-me, subi no ônibus em Marrocos"_ e _"anotaram a data da maratona"_.

	

	
1. (Opcional) Pesquise a classe `StringBuilder` (ou `StringBuffer` no Java 1.4).
	Ela é mutável. Por que usá-la em vez da `String`? Quando usá-la?

	Como você poderia reescrever o método de escrever a `String` de trás para a
	frente usando um `StringBuilder`?
	




## Desafio
1. Converta uma `String` para um número sem usar as bibliotecas do Java que já o
	fazem. Isto é, uma `String x = "762"` deve gerar um `int i = 762`.

	Para ajudar, saiba que um `char` pode ser transformado em `int` com o mesmo
	valor numérico fazendo:

	``` java
		char c = '3';
		int i = c - '0'; // i vale 3! 		
	```

	Aqui estamos nos aproveitando do conhecimento da tabela unicode:
	os números de 0 a 9 estão em sequência! Você poderia usar
	o método estático `Character.getNumericValue(char)` em vez disso.

	


## Discussão em aula: o que você precisa fazer em Java?

Qual é a sua necessidade com o Java? Precisa fazer algoritmos
de redes neurais? Gerar gráficos 3D? Relatórios em PDF? Gerar
código de barras e/ou boletos? Validar CPF? Mexer com
um arquivo do Excel?

O instrutor mostrará que, para a maioria absoluta das suas
necessidades, alguém já fez uma biblioteca e a disponibilizou.


