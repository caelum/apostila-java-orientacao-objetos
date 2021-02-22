# Resoluções de Exercícios

## Exercícios 3.3: Variáveis e tipos primitivos

1. Na empresa onde trabalhamos, há tabelas com o quanto foi gasto em cada mês. Para fechar o balanço do
	primeiro trimestre, precisamos somar o gasto total. Sabendo que, em Janeiro, foram gastos 15000
	reais, em Fevereiro, 23000 reais e em Março, 17000 reais, faça um programa que calcule e imprima o
	gasto total no trimestre e a média mensal de gastos. Siga esses passos:

	* Crie uma classe chamada `BalancoTrimestral` com um bloco main, como nos
	exemplos anteriores;
	* Dentro do `main` (o miolo do programa), declare uma variável inteira chamada
	`gastosJaneiro` e inicialize-a com 15000;
	* Crie também as variáveis `gastosFevereiro` e `gastosMarco`, inicializando-as
	com 23000 e 17000, respectivamente, utilize uma linha para cada declaração;
	* Crie uma variável chamada `gastosTrimestre` e inicialize-a com a soma das outras 3 variáveis;
	* Crie uma variável chamada `mediaPorMes` e inicialize-a com a divisão de `gastosTrimestre` por 3.
	* Imprima a variável `gastosTrimestre`.
	
	*Abaixo o código completo:*
	
	```java
    class BalancoTrimestral {
        public static void main(String[] args) {
            int gastosJaneiro = 15000;
            int gastosFevereiro = 23000;
            int gastosMarco = 17000;
            int gastosTrimestre = gastosJaneiro + gastosFevereiro + gastosMarco;

            System.out.println("Gasto do trimestre: R$" + gastosTrimestre);
            int mediaPorMes = gastosTrimestre / 3;
            System.out.println("Média mensal: R$" + mediaPorMes);
        }
    }
	```

## Exercícios 3.13: Fixação de sintaxe

Mais exercícios de fixação de sintaxe. Para quem já conhece um pouco de Java, pode ser muito simples;
mas recomendamos fortemente que você faça os exercícios para se acostumar com erros de compilação,
mensagens do javac, convenção de código, etc...

Apesar de extremamente simples, precisamos praticar a sintaxe que estamos aprendendo. Para cada
exercício, crie um novo arquivo com extensão **.java**, e declare aquele estranho cabeçalho, dando nome
a uma classe e com um bloco `main` dentro dele:

``` java
class ExercicioX {
	public static void main(String[] args) {
		// seu exercício vai aqui
	}
}
```

Não copie e cole de um exercício já existente! Aproveite para praticar.
1. Imprima todos os números de 150 a 300.
	
	``` java
		class ImprimeIntervalo {
			public static void main(String[] args) {
				int i = 150;
				while (i<=300){
					System.out.println(i);
					i++;
				}
			}
		}
	```
	ou
	``` java
		class ImprimeIntervalo {
			public static void main(String[] args) {
				for (int i = 150; i<=300; i++){
					System.out.println(i);
				}
			}
		}
	```
	
1. Imprima a soma de 1 até 1000.
	

	``` java
		class ImprimeSoma {
			public static void main(String[] args) {
				int soma = 0;
				int i = 1;
				while (i<=1000){
					soma = soma + i;
                    i++;
				}
				System.out.println(i);
			}
		}
	```
	ou
	``` java
		class ImprimeSoma {
			public static void main(String[] args) {
				soma = 0;
				for (int i = 1; i<=1000; i++){
					soma = soma + i;
				}
				System.out.println(i);
			}
		}
	```
	
1. Imprima todos os múltiplos de 3, entre 1 e 100.
	

	```java
		class MultiplosDeTresAteCem {
			public static void main (String[] args) {
				for (int i = 1; i < 100; i++ ){
					if (i % 3 == 0)	{
						System.out.println(i);
					}
				}
			}
		}
	```
	ou, entre outras tantas opções, a mais simples:
	```
		class MultiplosDeTresAteCem {
			public static void main (String[] args) {
				for (int i = 1; i < 100; i += 3 ){
					System.out.println(i);
				}
			}
		}
	```
	
1. Imprima os fatoriais de 1 a 10.

	O fatorial de um número n é n \* (n-1) \* (n-2) \* ... \* 1. Lembre-se de utilizar os parênteses.

	O fatorial de 0 é 1

	O fatorial de 1 é (0!) * 1 = 1

	O fatorial de 2 é (1!) * 2 = 2

	O fatorial de 3 é (2!) * 3 = 6

	O fatorial de 4 é (3!) * 4 = 24

	Faça um for que inicie uma variável n (número) como 1 e fatorial (resultado)
	como 1 e varia n de 1 até 10:

	``` java
	int fatorial = 1;
	for (int n = 1; n <= 10; n++) {

	}
	```

	``` java
		class Fatorial {
			public static void main (String[] args) {
				int fatorial = 1;
				for (int n = 1; n <= 10; n++) {
					fatorial = fatorial * n;
					System.out.println("fat(" + n + ") = " + fatorial);
				}
			}
		}
	```
	
1. No código do exercício anterior, aumente a quantidade de números que terão os
	fatoriais impressos, até 20, 30, 40. Em um  determinado momento, além desse
	cálculo demorar, vai começar a mostrar respostas completamente erradas.
	Por quê?

	Mude de `int` para `long` para ver alguma mudança.

	*Resposta:*

	Isso acontece porque, a partir de 16!, o valor supera o limite superior do
	tipo `int`. O tipo `long` consegue armazenar o cálculo dos fatoriais
	até 21!. Teste!
	
1. (opcional) Imprima os primeiros números da série de Fibonacci até passar de 100.
	A série de Fibonacci é a seguinte: 0, 1, 1, 2, 3, 5, 8, 13, 21, etc...
	Para calculá-la, o primeiro elemento vale 0, o segundo vale 1, daí por diante,
	o n-ésimo elemento vale o (n-1)-ésimo elemento somado ao (n-2)-ésimo elemento
	(ex: 8 = 5 + 3).
	
	``` java
		class Fibonacci {
			public static void main(String[] args) {
				int anterior = 0;
				int atual = 1;
				while (atual < 100) {
					System.out.println(atual);
					int proximo = anterior + atual;
					anterior = atual;
					atual = proximo;
				}
				System.out.println(atual);
			}
		}
	```
	
1. (opcional) Escreva um programa que, dada uma variável `x` com algum valor
	inteiro, temos um novo `x` de acordo com a seguinte regra:

	* se `x` é par, `x = x / 2`
	* se `x` é impar, `x = 3 * x + 1`
	* imprime `x`
	* O programa deve parar quando `x` tiver o valor final de 1. Por exemplo,
	para `x = 13`, a saída será:

	40 -> 20 -> 10 -> 5 -> 16 -> 8 -> 4 -> 2 -> 1

	> **Imprimindo sem pular linha**
	>
	> Um detalhe importante é que uma quebra de linha é impressa toda vez que
	> chamamos `println`. Para não pular uma linha, usamos o código a seguir:
	>
	> ``` java
	> 			System.out.print(variavel);
	> ```

	
	
	``` java
		class TresNMaisUm {
			public static void main(String[] args) {
				int x = 13;
				System.out.println("Iniciando...\n" + x);
				while (x != 1) {
					if (x % 2 == 0) {
						x = x / 2;
					} else {
						x = 3 * x + 1;
					}
					System.out.println(x);
				}
			}
		}
	```

	
1. (opcional)  Imprima a seguinte tabela, usando `for`s encadeados:
	```
	1
	2 4
	3 6 9
	4 8 12 16
	n n*2 n*3 .... n*n
	```

	``` java
		class Triangulo {
			public static void main(String[] args) {
				int numero = 5;
				for (int linha = 1; linha <= numero; linha++) {
					for (int coluna = 1; coluna <= linha; coluna++) {
						System.out.print(linha * coluna + " ");
					}
					System.out.println();
				}
			}
		}
	```

## Desafios 3.14: Fibonacci
1. Faça o exercício da série de Fibonacci usando apenas duas variáveis.

	``` java
		class Desafio {
			public static void main(String[] args) {
				int anterior = 0;
				int atual = 1;
				while (atual < 100) {
					System.out.println(atual);
					atual = anterior + atual;
					anterior = atual - anterior;
				}
				System.out.println(atual);
			}
		}
	```

## Exercícios 4.12: Orientação a Objetos
O modelo da conta a seguir será utilizado para os exercícios dos próximos capítulos.

O objetivo aqui é criar um sistema para gerenciar as contas de um `Banco`. __Os exercícios desse capítulo são extremamente importantes__.

1. Modele uma conta. A ideia aqui é apenas modelar, isto é, só identifique que informações são importantes. Desenhe no papel tudo o que uma `Conta` tem e tudo o que ela faz.
	Ela deve ter o nome do titular (`String`), o número (`int`), a agência (`String`), o saldo (`double`) e uma data de abertura (`String`). Além disso, ela deve fazer as seguintes ações: saca, para retirar um valor do saldo; deposita, para adicionar um valor ao saldo; calculaRendimento, para devolver o rendimento mensal dessa conta, que é de 10% sobre o saldo.

	*Resposta:*

	Modelando uma conta

	Toda conta **tem**:

	* String titular;
	* int numero;
    * String agencia;
	* double saldo;
	* String dataDeAbertura;

	Toda conta **faz**:
	* `saca`: retira uma determinada quantia do saldo da conta
	* `deposita`: adiciona uma determinada quantia no saldo da conta
	* `calculaRendimento`: devolve o quanto essa conta rende por mês

	

1. Transforme o modelo acima em uma classe Java. Teste-a, usando uma outra classe que tenha o `main`. Você deve criar a classe da conta com o nome `Conta`, mas pode nomear como quiser a classe de testes, por exemplo pode chamá-la `TestaConta`, contudo, ela
	deve necessariamente possuir o método `main`.

	A classe Conta deve conter, além dos atributos mencionados anteriormente, pelo menos os seguintes métodos:

	* `saca` que recebe um `valor` como parâmetro e retira esse valor do saldo da conta
	* `deposita` que recebe um `valor` como parâmetro e adiciona esse valor ao saldo da conta
	* `calculaRendimento` que não recebe parâmetro algum e devolve o valor do saldo multiplicado por 0.1

	Um esboço da classe:

	``` java
		class Conta {

			double saldo;
			// seus outros atributos e métodos

			void saca(double valor) {
				// o que fazer aqui dentro?
			}

			void deposita(double valor) {
				// o que fazer aqui dentro?
			}

			double calculaRendimento() {
				// o que fazer aqui dentro?
			}
		}
	```

	Você pode (e deve) compilar seu arquivo java sem que você ainda tenha terminado sua classe `Conta`. Isso evitará que você receba dezenas de erros de compilação de uma vez só. Crie a classe `Conta`, coloque seus atributos
	e, antes de colocar qualquer método, compile o arquivo java. O arquivo
	`Conta.class` será gerado, mas não podemos "executá-lo" já que essa
	classe não tem um `main`. De qualquer forma, a vantagem é que assim
	verificamos que nossa classe `Conta` já está tomando forma e está
	escrita em sintaxe correta.

	Esse é um processo incremental. Procure desenvolver assim seus exercícios, para não descobrir só no fim do caminho que algo estava muito errado.

	Um esboço da classe que possui o `main`:

	``` java
		class TestaConta {

			public static void main(String[] args) {
				Conta c1 = new Conta();

				c1.titular = "Hugo";
				c1.numero = 123;
				c1.agencia = "45678-9";
				c1.saldo = 50.0;
				c1.dataDeAbertura = "04/06/2015";

				c1.deposita(100.0);
				System.out.println("saldo atual:" + c1.saldo);
				System.out.println("rendimento mensal:" + c1.calculaRendimento());
			}
		}
	```
	Incremente essa classe. Faça outros testes, imprima outros atributos e invoque
	os métodos que você criou a mais.

	Lembre-se de seguir a convenção java, isso é importantíssimo. Isto é, preste
	atenção nas maiúsculas e minúsculas, seguindo o seguinte exemplo:
	`nomeDeAtributo`, `nomeDeMetodo`, `nomeDeVariavel`, `NomeDeClasse`,
	etc...

	> **Todas as classes no mesmo arquivo?**
	>
	> Você até pode colocar todas as classes no mesmo arquivo e apenas compilar
	> esse arquivo. Ele vai gerar um `.class` para cada classe presente nele.
	>
	> Porém, por uma questão de organização, é boa prática criar um arquivo
	> `.java` para cada classe. Em capítulos posteriores, veremos também
	> determinados casos nos quais você será **obrigado** a declarar cada classe
	> em um arquivo separado.
	>
	> Essa separação não é importante nesse momento do aprendizado, mas se quiser
	> ir praticando sem ter que compilar classe por classe, você pode dizer
	> para o `javac` compilar todos os arquivos java de uma vez:
	>
	> ```javac *.java```

	

	*Abaixo a resposta completa deste item:*
	
	``` java
		class Conta {
			String titular;
			int numero;
			String agencia;
			double saldo;
			String dataDeAbertura;

			void saca (double valor) {
				this.saldo -= valor;
			}

			void deposita (double valor) {
				this.saldo += valor;
			}

			double calculaRendimento() {
				return this.saldo * 0.1;
			}
		}
	```

1. Na classe Conta, crie um método `recuperaDadosParaImpressao()`, que não recebe parâmetro mas devolve o texto com todas as informações da nossa conta para efetuarmos a impressão.

	Dessa maneira, você não precisa ficar copiando e colando um monte de `System.out.println()` para cada mudança e teste que fizer com cada um de seus funcionários, você simplesmente vai fazer:

	``` java
		Conta c1 = new Conta();
		// brincadeiras com c1....
		System.out.println(c1.recuperaDadosParaImpressao());
	```

	Veremos mais a frente o método `toString`, que é uma solução muito mais
	elegante para mostrar a representação de um objeto como `String`, além de
	não jogar tudo pro `System.out` (só se você desejar).

	O esqueleto do método ficaria assim:

	``` java
		class Conta {

			// seus outros atributos e métodos

			String recuperaDadosParaImpressao() {
				String dados = "Titular: " + this.titular;
				dados += "\nNúmero: " + this.numero;
				// imprimir aqui os outros atributos...
				// também pode imprimir this.calculaRendimento()
				return dados;
			}
		}
	```

	*Abaixo a resposta completa deste item:*

	``` java
		class Conta {
			// outros atributos e métodos...

			String recuperaDadosParaImpressao() {
				String dados = "Titular: " + this.titular;
				dados += "\nNúmero: " + this.numero;
				dados += "\nAgência: " + this.agencia;
				dados += "\nSaldo: R$" + this.saldo;
				dados += "\nData de abertura: " + this.dataDeAbertura;
				return dados;
			}
		}
	```

1. Na classe de teste dentro do bloco main, construa duas contas com o `new` e compare-os com o `==`. E se eles
	tiverem os mesmos atributos? Para isso você vai precisar criar outra referência:

	``` java
		Conta c1 = new Conta();		
		c1.titular = "Danilo";
		c1.saldo = 100;

		Conta c2 = new Conta();		
		c2.titular = "Danilo";
		c2.saldo = 100;

		if (c1 == c2) {
			System.out.println("iguais");
		} else {
			System.out.println("diferentes"); 		
		}
	```

	Em ambos os casos, temos `false` como resposta. Isso é porque
	variáveis guardam apenas as referências! Por mais que dois objetos
	diferentes tenham as mesmas informações, cada um deles é um objeto
	à parte.

	Você pode ver isso de uma forma simples: se você alterar o `c1`,
	note que o `c2` não é alterado junto. Cada um é um objeto diferente
	e cada variável (`c1` e `c2`) referencia um deles.
	
1. Agora, crie duas referências para a **mesma** conta, compare-os com o `==`.
	Tire suas conclusões. Para criar duas referências pra mesma conta:

	``` java
		Conta c1 = new Conta():
		c1.titular = "Hugo";
		c1.saldo = 100;

		c2 = c1;
	```

	O que acontece com o `if` do exercício anterior?

	*Resposta:*

	Agora sim, obtemos true. Isso porque, de fato, ambas as variáveis têm
	referências para o mesmo objeto. Verifique: mude o titular da `c1` para _Mariana_ e imprima `c2.titular`. Você vai notar que o nome mudou!

1. (opcional) Em vez de utilizar uma `String` para representar a data, crie uma outra classe, chamada `Data`. Ela possui 3 campos `int`, para dia, mês e ano. Faça com que sua conta passe a usá-la. (é parecido com o último exemplo da explicação, em que a `Conta` passou a ter referência para um `Cliente`).

	``` java
		class Conta {
			Data dataDeAbertura; // qual é o valor default aqui?
			// seus outros atributos e métodos
		}

		class Data {
			int dia;
			int mes;
			int ano;
		}
	```

	Modifique sua classe `TestaConta` para que você crie uma `Data` e
	atribua ela a `Conta`:

	```java
		Conta c1 = new Conta();
		//...
		Data data = new Data(); // ligação!
		c1.dataDeAbertura = data;
	```

	Faça o desenho do estado da memória quando criarmos um `Conta`. Uma possibilidade é o arquivo `Data.java` ficar assim:

	```java
		class Data {
			int dia;
			int mes;
			int ano;

			void preencheData (int dia, int mes, int ano) {
				this.dia = dia;
				this.mes = mes;
				this.ano = ano;
			}
		}			
	```

	No arquivo `Conta.java`, altere o atributo para a data:

	```java
		class Conta {
			// outros atributos
			Data dataDeAbertura;

			// metodos
		}
	```

	Finalmente no arquivo `TestaConta.java`...

	``` java
		class TestaConta {
			public static void main(String[] args) {
				Conta c1 = new Conta();
				c1.titular = "Hugo";
				c1.saldo = 50;
				c1.deposita(100);

				// adicionando a data como tipo
				c1.dataDeAbertura = new Data();
				c1.dataDeAbertura.preencheData(1, 7, 2009);

				System.out.println(c1.recuperaDadosParaImpressao());
			}
		}
	```

1. (opcional) Modifique seu método `recuperaDadosParaImpressao` para que ele devolva o valor da `dataDeAbertura` daquela `Conta`:

	``` java
	class Conta {

		// seus outros atributos e métodos
		Data dataDeAbertura;

		String recuperaDadosParaImpressao() {
			String dados = "\nTitular: " + this.titular;
			// imprimir aqui os outros atributos...

			dados += "\nDia: " + this.dataDeAbertura.dia;
			dados += "\nMês: " + this.dataDeAbertura.mes;
			dados += "\nAno: " + this.dataDeAbertura.ano;
			return dados;
		}
	}
	```

	Teste-o. O que acontece se chamarmos o método `recuperaDadosParaImpressao` antes de atribuirmos uma data para esta `Conta`?
	
	*Resposta:* dia, mês e ano serão apresentados com o valor 0.

	``` java
	class TestaConta {
	public static void main(String[] args) {
		Conta c1 = new Conta();
		c1.titular = "Hugo";
		c1.agencia = "12-x";
		c1.numero = 557890;
		c1.saldo = 50;
		c1.deposita(100);
		// adicionando a data como tipo
		c1.dataDeAbertura = new Data();
		//chamando o método `recuperaDadosParaImpressao` antes de atribuirmos uma data para esta `Conta`
		System.out.println(c1.recuperaDadosParaImpressao());
		c1.dataDeAbertura.preencheData(1, 7, 2009);
	}
}
```
1. (opcional) O que acontece se você tentar acessar um atributo diretamente na
	classe? Como, por exemplo:

	``` java
		Conta.saldo = 1234;
	```

	Esse código faz sentido? E este:

	``` java
		Conta.calculaRendimento();
	```

	Faz sentido perguntar para o esquema da Conta seu valor anual?
1. (opcional-avançado) Crie um método na classe `Data` que devolva o valor
	formatado da data, isto é, devolva uma String com "dia/mes/ano". Isso para que
	o método `recuperaDadosParaImpressao` da classe `Conta` possa ficar assim:

	``` java
	class Conta {
		// atributos e metodos

		String recuperaDadosParaImpressao() {
			// imprime outros atributos...
			dados += "\nData de abertura: " + this.dataDeAbertura.formatada();
			return dados;
		}
	}
	```

	*Resposta:*

	``` java
		class Data {
			// atributos e método preencheData

			String formatada() {
				return this.dia + "/" + this.mes + "/" + this.ano;
			}
		}		
	```

## Desafios 4.13
1. Um método pode chamar ele mesmo. Chamamos isso de **recursão**. Você pode
	resolver a série de Fibonacci usando um método que chama ele mesmo. O objetivo
	é você criar uma classe, que possa ser usada da seguinte maneira:

	``` java
		Fibonacci fibonacci = new Fibonacci();
		for (int i = 1; i <= 6; i++) {
			int resultado = fibonacci.calculaFibonacci(i);
			System.out.println(resultado);
		}
	```

	Aqui imprimirá a sequência de Fibonacci até a sexta posição, isto é:
	1, 1, 2, 3, 5, 8.

	Este método `calculaFibonacci` não pode ter nenhum laço, só pode chamar ele
	mesmo como método. Pense nele como uma função, que usa a própria função para
	calcular o resultado.
	
	*Resposta*:
	
	``` java
		class Fibonacci{
			
			public int calculaFibonacci(int n) {
				if (n <= 2) {
					return 1;
				} else {
					return calculaFibonacci(n-1) + calculaFibonacci(n-2);
				}
			}
		}
	```
	
1. Por que o modo acima é extremamente mais lento para calcular a série do que o
	modo iterativo (que se usa um laço)?
	
	*Resposta:*
	
	Dessa forma, o código fica muito mais lento porque ele não consegue aproveitar
	os fibonaccis já calculados anteriormente. E, pior ainda, ele abre o cálculo
	de fibonaccis exponencialmente porque, para calcular o fibonacci de um número,
	é preciso somar os dois anteriores.
	
1. Escreva o método recursivo novamente, usando apenas uma linha. Para isso,
	pesquise sobre o **operador condicional ternário**. (ternary operator)
	
	*Resposta*:
	``` java
		public static int calculaFibonacci(int n) {
			return (n <= 2) ? 1 : calculaFibonacci(n-1) + calculaFibonacci(n-2);
		}
	```

## Exercícios 5.8: Encapsulamento, construtores e static


1. Adicione o modificador de visibilidade (`private`, se necessário) para cada
	atributo e método da classe `Conta`. Tente criar uma `Conta`
	no `main` e modificar ou ler um de seus atributos privados. O que acontece?

	

	

	``` java
		public class Conta {
			private String titular;
			private int numero;
			private String agencia;
			private double saldo;
			private Data dataDeAbertura;

			public void saca(double valor) {...}

			public void deposita(double valor) {...}

			public double calculaRendimento() {...}

			public String recuperaDadosParaImpressao() {...}
		}
	```

1. Crie apenas os getters e setters necessários da sua classe `Conta`. Pense sempre se é preciso criar
	cada um deles. Por exemplo:

	``` java
		class Conta {
			private String titular;

			// ...

			public String getTitular() {
				return this.titular;
			}

			public void setTitular(String titular) {
				this.titular = titular;
			}
		}
	```

	Não copie e cole! Aproveite para praticar sintaxe. Logo passaremos a usar
	o Eclipse e aí sim teremos procedimentos mais simples para este tipo de
	tarefa.

	Repare que o método `calculaRendimento` parece também um getter. Aliás,
	seria comum alguém nomeá-lo de `getRendimento`. Getters não precisam apenas
	retornar atributos. Eles podem trabalhar com esses dados.
	
	*Resposta completa para este item:*

	``` java
		public class Conta {
			private String titular;
			private int numero;
			private String agencia;
			private double saldo;
			private String dataDeAbertura;

			public double calculaRendimento() {
				return this.saldo * 0.1;
			}

			public String getTitular() {
				return this.titular;
			}

			public void setTitular (String titular) {
				this.titular = titular;
			}

			public int getNumero() {
				return this.numero;
			}

			public void setNumero (int numero) {
				this.numero = numero;
			}

			public String getAgencia() {
				return this.agencia;
			}

			public void setAgencia (String agencia) {
				this.agencia = agencia;
			}

			public double getSaldo() {
				return this.saldo;
			}

			public void deposita (double valor) {
				this.saldo += valor;
			}

			public void saca (double valor) {
				this.saldo -= valor;
			}

			public String getDataDeAbertura() {
				return this.dataDeAbertura;
			}

			public void setDataDeAbertura (String dataDeAbertura) {
				this.dataDeAbertura = dataDeAbertura;
			}
		}
	```

1. Altere suas classes que acessam e modificam atributos de uma `Conta` para utilizar os getters e setters recém criados.

	Por exemplo, onde você encontra:

	``` java
		c.titular = "Batman";
		System.out.println(c.titular);
	```

	passa para:

	``` java
		c.setTitular("Batman");
		System.out.println(c.getTitular());
	```

	*Resposta completa para este item:*

	``` java
		class TestaConta {
			public static void main(String[] args) {
				Conta c1 = new Conta("Hugo");
				c1.setNumero(123);
				c1.deposita(50);
				c1.setDataDeAbertura(new Data(1, 7, 2009));

				System.out.println(c1.recuperaDadosParaImpressao());
			}
		}
	```
	
1. Faça com que sua classe `Conta` possa receber, opcionalmente, o nome
	do titular da `Conta` durante a criação do objeto. Utilize construtores para obter esse resultado.

	Dica: utilize um construtor sem argumentos também, para o caso de a pessoa
	não querer passar o titular da `Conta`.

	Seria algo como:

	``` java
		class Conta {
			public Conta() {
				// construtor sem argumentos
			}

			public Conta(String titular) {
				// construtor que recebe o titular
			}
		}
	```

	Por que você precisa do construtor sem argumentos para que a passagem do nome
	seja opcional?
	
	*Resposta*: A partir do momento que declaramos um construtor, o construtor default não é mais fornecido, por isso se quisermos ter a passagem do nome como opcional, teremos que ter duas versões de construtores: uma que não exige nada como parâmetro e outra que exige uma String.

	``` java
		public class Conta {
			// atributos

			public Conta() {}

			public Conta(String titular) {
				this.titular = titular;
			}

			// métodos
		}
	```

1. (opcional) Adicione um atributo na classe `Conta` de tipo `int` que
	se chama identificador. Esse identificador deve ter um valor único para cada
	instância do tipo `Conta`. A primeira `Conta` instanciada tem
	identificador 1, a segunda 2, e assim por diante. Você deve utilizar os
	recursos aprendidos aqui para resolver esse problema.

	Crie um getter para o identificador. Devemos ter um setter?
	
	*Resposta*:

	``` java
		public class Conta {
			private int identificador;
			private static int proximoIdentificador;

			public Conta(String titular) {
				this.titular = titular;
				this.identificador = proximoIdentificador++;
			}

			public int getIdentificador() {
				return this.identificador;
			}

			// restante da classe
		}
	```

	Não faz sentido que o identificador tenha um setter já que, pela lógica
	da aplicação, o `identificador` é um número único para cada funcionário
	no sistema.
	
1. (opcional) Como garantir que datas como 31/2/2021 não sejam aceitas pela sua
	classe `Data`?
	
	*Resposta*: Você pode definir um construtor na classe Data que exija dia, mes e ano. Este construtor invoca o método `preencheData` o qual invoca o método `isDataViavel` que faz a validação das datas válidas. Nesse
	momento, a única forma de indicar que houve um erro que você aprendeu é
	imprimir uma mensagem no terminal avisando, mas, mais para a frente,
	veremos uma forma muito mais elegante de tratar esses casos.

	``` java
		public class Data {

			private int dia;
			private int mes;
			private int ano;

			public Data(int dia, int mes, int ano) {
				this.preencheData(dia, mes, ano);
			}

			private boolean isDataViavel(int dia, int mes, int ano) {
				if (dia <= 0 || mes <= 0) {
					return false;
				}

				int ultimoDiaDoMes = 31; // por padrao são 31 dias

				if (mes == 4 || mes == 6 || mes == 9 || mes == 11) {
					ultimoDiaDoMes = 30;
				} else if (mes == 2) {
					if (ano % 4 == 0) {
						ultimoDiaDoMes = 29;
					} else {
						ultimoDiaDoMes = 28;
					}
				}
				if (dia > ultimoDiaDoMes) {
					return false;
				}

				return true;
			}

			void preencheData(int dia, int mes, int ano) {
				if (!isDataViavel(dia, mes, ano)) {
					System.out.println("A data " + dia + "/" + mes + "/" + ano + " não existe!");
				} else {
					this.dia = dia;
					this.mes = mes;
					this.ano = ano;
				}
			}

			String formatada() {
				return this.dia + "/" + this.mes + "/" + this.ano;
			}
		}
	```
	Faça testes com datas válidas e inválidas:

	```java
	class TestaDataAberturaDaConta {

	public static void main(String[] args) {
		Conta c1 = new Conta();
		c1.setTitular("Hugo"); ;
		c1.setAgencia("12-x");;
		c1.setNumero(557890); ;
		c1.deposita(50);;
		c1.deposita(100);
		// adicionando a data como tipo
		c1.setDataDeAbertura(new Data(31, 2, 2021)); // teste também com datas válidas
		System.out.println(c1.recuperaDadosParaImpressao());
	}
}

	```


1. (opcional) Suponha que temos a classe `PessoaFisica` que tem um CPF como atributo.
	Como garantir que pessoa física alguma tenha CPF invalido,
	nem seja criada `PessoaFisica` sem cpf inicial?
	
	*Resposta*:
	(Suponha que já existe um algoritmo de validação de cpf:
	basta passar o cpf por um método `valida(String x)...`)
	
	Você pode fazer a validação ser chamada no construtor e, por ora,
	imprimir a mensagem no console. No capítulo 11 veremos uma forma de
	realmente impedir a criação do objeto, caso essa validação não passe.
	



## Desafios 5.9
1. Porque esse código não compila?

	``` java
		class Teste {
			int x = 37;
			public static void main(String [] args) {
				System.out.println(x);
			}
		}
	```
	
	*Resposta*:
	O `main` é um método estático, isto é: ele não é do objeto, é da classe.
	Já o atributo `x` não tem a palavra `static` e, portanto, é do objeto.

	Para rodar o `main`, não há necessidade (ou garantia) de que teremos um
	objeto do tipo `Teste`, então não há garantia de que o `x` sequer
	existirá.

1. Imagine que tenha uma classe `FabricaDeCarro` e quero garantir que só existe um
	objeto desse tipo em toda a memória. Não existe uma palavra chave especial para
	isto em Java, então teremos de fazer nossa classe de tal maneira que ela respeite
	essa nossa necessidade. Como fazer isso? (pesquise: singleton design pattern)

## Exercícios 8.9: Mostrando os dados da conta na tela

1. Crie a classe `ManipuladorDeContas` dentro do pacote `br.com.caelum.contas`. Repare
	que os pacotes `br.com.caelum.contas.main` e `br.com.caelum.contas.modelo` são
	subpacotes do pacote `br.com.caelum.contas`, portanto o pacote `br.com.caelum.contas`
	já existe. Para criar a classe neste pacote, basta selecioná-lo na janela de criação
	da classe:

	![ {w=70}](assets/images/javafx/manipulador.png)

	A classe `ManipuladorDeContas` fará a ligação da `Conta` com a tela, por isso precisaremos
	declarar um atributo do tipo `Conta`.

	

	

	

1. Crie o método `criaConta` que recebe como parâmetro um objeto do tipo `Evento`.
	Instancie uma conta para o atributo `conta` e coloque os valores de `numero`,
	`agencia` e `titular`. Algo como:

	``` java
	public class ManipuladorDeContas {

	private Conta conta;
	
    public void criaConta(Evento evento){
        this.conta = new Conta();
        this.conta.setTitular("Batman");
        // faça o mesmo para os outros atributos
    }
	```
1. Com a conta instanciada, agora podemos implementar as funcionalidades de saque e
	depósito. Crie o método `deposita` que recebe um `Evento`, que é a classe que
	retorna os dados da tela nos tipos que precisamos. Por exemplo, se quisermos o
	valor a depositar sabemos que ele é do tipo `double` e que o nome do campo na
	tela é `valor` então podemos fazer:

	``` java
    public void deposita(Evento evento){
        double valorDigitado = evento.getDouble("valor");
        this.conta.deposita(valorDigitado);
    }
	```
1. Crie agora o método `saca`. Ele também deve receber um `Evento` nos mesmos
	moldes do `deposita`.

	``` java
	public void saca(Evento evento){
		double valorDigitado = evento.getDouble("valor");
		this.conta.saca(valorDigitado);
	}
	```
	
1. Precisamos agora testar nossa aplicação, crie a classe `TestaContas` dentro do
	pacote `br.com.caelum.contas` com um `main`. Nela vamos chamar o `main` da
	classe `TelaDeContas` que mostrará a tela de nosso sistema. Não se esqueça de
	fazer o import desta classe!

	``` java
    import br.com.caelum.javafx.api.main.TelaDeContas;

    public class TestaContas {

        public static void main(String[] args) {
            TelaDeContas.main(args);
        }
    }
	```

	Rode a aplicação, crie a conta e tente fazer as operações de saque e depósito. Tudo
	deve funcionar normalmente.

## Exercícios 9.7: Herança e Polimorfismo
1. Vamos ter mais de um tipo de conta no nosso sistema então vamos precisar de uma nova tela para cadastrar os diferentes tipos de conta. Essa tela já está pronta e para utilizá-la só precisamos alterar a classe que estamos chamando no método `main()` no `TestaContas.java`:

	``` java
    package br.com.caelum.contas.main;

    import br.com.caelum.javafx.api.main.SistemaBancario;

    public class TestaContas {

        public static void main(String[] args) {
            SistemaBancario.mostraTela(false);
            // TelaDeContas.main(args);
        }
    }		
	```
1. Ao rodar a classe `TestaContas` agora, teremos a tela abaixo:

	![ {w=50}](assets/images/javafx/tela-inicial.png)

	Vamos entrar na tela de criação de contas para vermos o que precisamos implementar para que o sistema funcione. Para isso, clique no botão **Nova Conta**. A seguinte tela aparecerá:

	![ {w=50}](assets/images/javafx/nova-conta.png)

	Podemos perceber que além das informações que já tínhamos na conta, temos agora o tipo: se queremos uma conta corrente ou uma conta poupança. Vamos então criar as classes correspondentes.

	* Crie a classe `ContaCorrente` no pacote `br.com.caelum.contas.modelo` e faça com que ela seja filha da classe `Conta`
	* Crie a classe `ContaPoupanca` no pacote `br.com.caelum.contas.modelo` e faça com que ela seja filha da classe `Conta`
1. Precisamos pegar os dados da tela para conseguirmos criar a conta correspondente. No
	`ManipuladorDeContas` vamos alterar o método `criaConta`. Atualmente, apenas
	criamos uma nova conta com os dados direto no código.
	Vamos fazer com que agora os dados sejam recuperados da tela para colocarmos na nova
	conta, faremos isso utilizando o objeto `evento`:

	``` java

	public void criaConta(Evento evento) {
      	this.conta = new Conta();
      	this.conta.setAgencia(evento.getString("agencia"));
      	this.conta.setNumero(evento.getInt("numero"));
      	this.conta.setTitular(evento.getString("titular"));
  	}
	```

	Mas precisamos dizer qual tipo de conta que queremos criar! Devemos então recuperar o tipo da conta escolhido e criar a conta correspondente. Para isso, ao invés de criar um objeto do tipo 'Conta', vamos usar o método `getSelecionadoNoRadio` do objeto `evento` para pegar o tipo, fazer um `if` para verificar esse tipo e só depois criar o objeto do tipo correspondente. Após essas mudanças, o método `criaConta` ficará como abaixo:

	``` java
  	public void criaConta(Evento evento) {
      	String tipo = evento.getSelecionadoNoRadio("tipo");
      	if (tipo.equals("Conta Corrente")) {
          this.conta = new ContaCorrente();
      	} else if (tipo.equals("Conta Poupança")) {
          this.conta = new ContaPoupanca();
     	}
      	this.conta.setAgencia(evento.getString("agencia"));
      	this.conta.setNumero(evento.getInt("numero"));
      	this.conta.setTitular(evento.getString("titular"));
 	 }
	```
1. Apesar de já conseguirmos criar os dois tipos de contas, nossa lista não consegue exibir o tipo de cada conta na lista da tela inicial. Para resolver isso, podemos criar um método `getTipo` em cada uma de nossas contas fazendo com que a conta corrente devolva a string "Conta Corrente" e a conta poupança devolva a string "Conta Poupança":

	``` java
	public class ContaCorrente extends Conta {
		public String getTipo() {
			return "Conta Corrente";
		}
	}

	public class ContaPoupanca extends Conta {
		public String getTipo() {
			return "Conta Poupança";
		}
	}
	```
1. Altere os métodos `saca` e `deposita` para buscarem o campo `valorOperacao` ao
	invés de apenas `valor` na classe `ManipuladorDeContas`.

1. Vamos mudar o comportamento da operação de saque de acordo com o tipo de conta que estiver sendo utilizada. Na classe `ManipuladorDeContas` vamos alterar o método `saca` para tirar 10 centavos de cada saque em uma conta corrente:

	``` java
    public void saca(Evento evento) {
        double valor = evento.getDouble("valorOperacao");
        if (this.conta.getTipo().equals("Conta Corrente")){
            this.conta.saca(valor + 0.10);
        } else {
            this.conta.saca(valor);
        }
    }
	```

	Ao tentarmos chamar o método `getTipo`, o Eclipse reclamou que esse método não existe na classe `Conta` apesar de existir nas classes filhas. Como estamos tratando todas as contas genericamente, só conseguimos acessar os métodos da classe mãe. Vamos então colocá-lo na classe `Conta`:

	``` java
    public class Conta {
        public String getTipo() {
        	return "Conta";
        }
    }
	```
1. Agora o código compila mas temos um outro problema. A lógica do nosso saque vazou para a classe `ManipuladorDeContas`. Se algum dia precisarmos alterar o valor da taxa no saque, teríamos que mudar em todos os lugares onde fazemos uso do método `saca`. Esta lógica deveria estar encapsulada dentro do método `saca` de cada conta. Vamos então sobrescrever o método dentro da classe `ContaCorrente`:

	``` java
	public class ContaCorrente extends Conta {
	    @Override
	    public void saca(double valor) {
	        this.saldo -= (valor + 0.10);
	    }

      // restante da classe
	}
	```

	Repare que, para acessar o atributo saldo herdado da classe `Conta`, **você vai precisar mudar o modificador de visibilidade de saldo para `protected`**.

	Agora que a lógica está encapsulada, podemos corrigir o método `saca` da classe `ManipuladorDeContas`:

	``` java
    public void saca(Evento evento) {
        double valor = evento.getDouble("valorOperacao");
        this.conta.saca(valor);
    }
	```

	Perceba que agora tratamos a conta de forma genérica!
1. Rode a classe `TestaContas`, adicione uma conta de cada tipo e veja se o tipo é apresentado corretamente na lista de contas da tela inicial.

	Agora, clique na conta corrente apresentada na lista para abrir a tela de detalhes de contas. Teste as operações de saque e depósito e perceba que a conta apresenta o comportamento de uma conta corrente conforme o esperado.

	E se tentarmos realizar uma transferência da conta corrente para a conta poupança? O que acontece?
1. Vamos começar implementando o método `transfere` na classe `Conta`:

	``` java
    public void transfere(double valor, Conta conta) {
        this.saca(valor);
        conta.deposita(valor);
    }
	```

	Também precisamos implementar o método `transfere` na classe `ManipuladorDeContas` para fazer o vínculo entre a tela e a classe `Conta`:

	``` java
    public void transfere(Evento evento) {
        Conta destino = (Conta) evento.getSelecionadoNoCombo("destino");
        conta.transfere(evento.getDouble("valorTransferencia"), destino);
    }
	```

	Rode de novo a aplicação e teste a operação de transferência.
1. Considere o código abaixo:

	``` java
		Conta c = new Conta();
		ContaCorrente cc = new ContaCorrente();
		ContaPoupanca cp = new ContaPoupanca();
	```

	Se mudarmos esse código para:

	``` java
		Conta c = new Conta();
		Conta cc = new ContaCorrente();
		Conta cp = new ContaPoupanca();
	```

	Compila? Roda? O que muda? Qual é a utilidade disso? Realmente, essa não é
	a maneira mais útil do polimorfismo. Porém existe uma utilidade de declararmos uma variável de um tipo
	menos específico do que o objeto realmente é, como fazemos na classe `ManipuladorDeContas`.

	É **extremamente importante** perceber que não importa como nos referimos a
	um objeto, o método que será invocado é sempre o mesmo! A JVM vai descobrir em
	tempo de execução qual deve ser invocado, dependendo de que tipo é aquele objeto,
	não importando como nos referimos a ele.
1. (Opcional)
	A nossa classe `Conta` devolve a palavra "Conta" no método `getTipo`. Use a palavra chave `super` nos métodos `getTipo` reescritos nas classes filhas,
	para não ter de reescrever a palavra "Conta" ao devolver os tipos "Conta Corrente" e "Conta Poupança".

	``` java
		class ContaCorrente extends Conta {

			public String getTipo() {
				return super.getTipo() + " Corrente";
			}
		}
	```

	E, também

	``` java
		class ContaPoupanca extends Conta {

			public String getTipo() {
				return super.getTipo() + " Poupança";
			}
			//...
		}
	```

1. (Opcional) Se você precisasse criar uma classe `ContaInvestimento`, e seu
	método `saca` fosse complicadíssimo, você precisaria alterar a classe
	`ManipuladorDeContas`?

	*Resposta:*
	Não! Essa é a vantagem do polimorfismo: qualquer coisa que **seja uma** Conta
	pode ser passada para o método `saca`. A complexidade fica isolada, dentro
	de cada classe.
	

## Exercícios 11.5: Interfaces
1. Nosso banco precisa tributar dinheiro de alguns bens que nossos clientes possuem.
	Para isso vamos criar uma interface no pacote `br.com.caelum.contas.modelo` do nosso projeto
	 `fj11-contas` já existente:

	``` java
	public interface Tributavel {
      public double getValorImposto();
	}
	```

	Lemos essa interface da seguinte maneira: "todos que quiserem ser _tributável_
	precisam saber retornar _o valor do imposto_, devolvendo um double".

	Alguns bens são tributáveis e outros não, `ContaPoupanca` não é tributável,
	já para `ContaCorrente` você precisa pagar 1% da conta e o `SeguroDeVida`
	tem uma taxa fixa de 42 reais mais 2% do valor do seguro.

	Aproveite o Eclipse! Quando você escrever `implements Tributavel` na classe
	`ContaCorrente`, o _quick fix_ do Eclipse vai sugerir que você reescreva
	o método; escolha essa opção e, depois, preencha o corpo do método adequadamente:

	``` java
	public class ContaCorrente extends Conta implements Tributavel {

		// outros atributos e métodos

		public double getValorImposto() {
			return this.getSaldo() * 0.01;
		}
	}
	```

	Crie a classe `SeguroDeVida`, aproveitando novamente do Eclipse, para obter:

	``` java
	public class SeguroDeVida implements Tributavel {
		private double valor;
		private String titular;
		private int numeroApolice;

		public double getValorImposto() {
			return 42 + this.valor * 0.02;
		}

    // getters e setters para os atributos
	}
	```
	Além disso, escreva o método `getTipo` para que o tipo do produto apareça na interface gráfica:
	``` java
	public String getTipo(){
		return "Seguro de Vida";
	}
	```

1. Vamos criar a classe `ManipuladorDeSeguroDeVida` dentro do pacote
	`br.com.caelum.contas` para vincular a classe `SeguroDeVida` com a tela de criação
	de seguros. Esta classe deve ter um atributo do tipo `SeguroDeVida`.

	Crie também o método `criaSeguro` que deve receber um parâmetro do tipo
	`Evento` para conseguir obter os dados da tela. Você deve pegar os parâmetros
	"numeroApolice" do tipo `int`, "titular" do tipo `String` e "valor" do tipo
	`double`.

	O código final deve ficar parecido com o código abaixo:

	``` java
  	package br.com.caelum.contas;

  	import br.com.caelum.contas.modelo.SeguroDeVida;
  	import br.com.caelum.javafx.api.util.Evento;

  	public class ManipuladorDeSeguroDeVida {

    	private SeguroDeVida seguroDeVida;

    	public void criaSeguro(Evento evento){
      		this.seguroDeVida = new SeguroDeVida();
      		this.seguroDeVida.setNumeroApolice(evento.getInt("numeroApolice"));
      		this.seguroDeVida.setTitular(evento.getString("titular"));
      		this.seguroDeVida.setValor(evento.getDouble("valor"));
    	}
  	}
	```
1. Execute a classe `TestaContas` e tente cadastrar um novo seguro de vida. O seguro
	cadastrado deve aparecer na tabela de seguros de vida.

1. Queremos agora saber qual o valor total dos impostos de todos os tributáveis.
	Vamos então criar a classe `ManipuladorDeTributaveis` dentro do pacote
	`br.com.caelum.contas`.
	Crie também o método `calculaImpostos` que recebe um parâmetro do tipo `Evento`:

	``` java
  	package br.com.caelum.contas;

  	import br.com.caelum.javafx.api.util.Evento;

  	public class ManipuladorDeTributaveis {

    	public void calculaImpostos(Evento evento){
    	  // aqui calcularemos o total
    	}
  	}
	```

1. Agora que criamos o tributavel, vamos habilitar a última aba de nosso sistema. Altere
	a classe `TestaContas` para passar o valor `true` na chamada do método
	`mostraTela`.
  Observe que agora que temos o seguro de vida funcionando, a tela de relatório já
	consegue imprimir o valor dos impostos individuais de cada tipo de _Tributavel_.

1. No método `calculaImpostos` precisamos buscar os valores de impostos de cada `Tributavel` e
	somá-los. Para saber a quantidade de tributáveis, a classe `Evento` possui um
	método chamado `getTamanhoDaLista` que deve receber o nome da lista desejada, no
	caso "listaTributaveis". Existe também um outro método que retorna um `Tributavel` de uma
	determinada posição de uma lista, onde precisamos passar o nome da lista e o índice
	do elemento. Precisamos percorrer a lista inteira, passando por cada posição então
	utilizaremos um `for` para isto.

	``` java
  	package br.com.caelum.contas;

  	import br.com.caelum.contas.modelo.Tributavel;
  	import br.com.caelum.javafx.api.util.Evento;

  	public class ManipuladorDeTributaveis {

   	 	private double total;

    	public void calculaImpostos(Evento evento){
      		total = 0;
      		int tamanho = evento.getTamanhoDaLista("listaTributaveis");
      		for (int i = 0; i < tamanho; i++) {
        		Tributavel t = evento.getTributavel("listaTributaveis", i);
        		total += t.getValorImposto();
      		}
    	}

    	public double getTotal() {
      		return total;
    	}
  	}
	```

	Repare que, de dentro do `ManipuladorDeTributaveis`, você não pode acessar
	o método `getSaldo`, por exemplo, pois você não tem a garantia de que o
	`Tributavel` que vai ser passado como argumento tem esse método. A única
	certeza que você tem é de que esse objeto tem os métodos declarados na
	interface `Tributavel`.

	É interessante enxergar que as interfaces (como aqui, no caso, `Tributavel`)
	costumam ligar classes muito distintas, unindo-as por uma característica que elas
	tem em comum. No nosso exemplo, `SeguroDeVida` e `ContaCorrente` são
	entidades completamente distintas, porém ambas possuem a característica de serem
	tributáveis.

	Se amanhã o governo começar a tributar até mesmo `PlanoDeCapitalizacao`, basta
	que essa classe implemente a interface `Tributavel`! Repare no grau de
	desacoplamento que temos: a classe `GerenciadorDeImpostoDeRenda` nem imagina
	que vai trabalhar como  `PlanoDeCapitalizacao`. Para ela, o único fato que
	importa é que o objeto respeite o contrato de um tributável, isso é, a interface
	`Tributavel`. Novamente: programe voltado à interface, não à implementação.

	Quais os benefícios de manter o código com baixo acoplamento?
	
    *Resposta:*

	Quanto menos acoplado o código, mais fácil é sua manutenção, já que alterar
	uma classe não deve atrapalhar o funcionamento das outras. Note que o uso de
	interfaces cria uma ligação entre tipos que permite o **polimorfismo**, mas
	é bem menos intrusivo do que a herança: não é possível reaproveitar código da
	mãe.

	Por um lado, isso pode parecer negativo e, por vezes, teremos um trecho de
	código repetido. Mas a certeza de que, ao mudar uma classe, não afetaremos as
	outras, é muito confortável. Para usar interfaces **e** evitar a repetição,
	procure pelo conceito de **composição**.

1. (opcional) Crie a classe `TestaTributavel` com um método `main` para testar
	o nosso exemplo:

	``` java
	public class TestaTributavel {

		public static void main(String[] args) {
			ContaCorrente cc = new ContaCorrente();
			cc.deposita(100);
			System.out.println(cc.getValorImposto());

			// testando polimorfismo:
			Tributavel t = cc;
			System.out.println(t.getValorImposto());
		}
	}
	```

	Tente chamar o método `getSaldo` através da referência `t`, o que ocorre?
	Por quê?
	
	A linha em que atribuímos `cc` a um `Tributavel` é apenas para você enxergar
	que é possível fazê-lo. Nesse nosso caso, isso não tem uma utilidade. Essa
	possibilidade foi útil no exercício anterior.

	

	*Resposta*: Apesar de ser um objeto do tipo `ContaCorrente`, ao chamarmos ele de
	`Tributavel`, apenas garantimos para o compilador que aquele objeto tem
	os métodos que **todo** `Tributavel` tem. E como o compilador do Java só
	trabalha com certezas, ele só permite chamar os métodos definidos no tipo
	da variável.
	
## Exercícios opcionais 11.6
**Atenção**: caso você faça esse exercício, faça isso num projeto à parte
`conta-interface` já que usaremos a `Conta` como classe em exercícios futuros.
1. (Opcional) Transforme a classe `Conta` em uma interface.

	

	``` java
	public interface Conta {
		public double getSaldo();
		public void deposita(double valor);
		public void saca(double valor);
		public void atualiza(double taxaSelic);
	}
	```

	Adapte `ContaCorrente` e `ContaPoupanca` para essa modificação:

	```java
	public class ContaCorrente implements Conta {
		// ...
	}
	```

	```java
	public class ContaPoupanca implements Conta {
		// ...
		}
	```

	Algum código vai ter de ser copiado e colado? Isso é tão ruim?
		
	Ao fim desse exercício você terá os seguintes códigos:

	``` java
	public interface Conta {

		public abstract void deposita(double valor);
		public abstract void saca(double valor);
		public abstract double getSaldo();
		public abstract void atualiza(double taxa);
	}
	```

	E as classes que implementam `Conta`:

	``` java
	public class ContaCorrente implements Conta, Tributavel {
		private double saldo;

		@Override
		public void deposita(double valor) {
			this.saldo += valor;
		}

		@Override
		public void saca(double valor) {
			this.saldo -= valor;
		}

		@Override
		public double getSaldo() {
			return this.saldo;
		}

		@Override
		public void atualiza(double taxa) {
			this.saldo += this.saldo * taxa * 2;
		}

		@Override
		public double calculaTributos() {
			return this.saldo * 0.01;
		}
	}
	```

	``` java
	public class ContaPoupanca implements Conta {
		private double saldo;

		@Override
		public void atualiza(double taxa) {
			this.saldo += this.saldo * taxa * 3;
		}

		@Override
		public void deposita(double valor) {
			this.saldo += (valor - 0.1);
		}

		@Override
		public void saca(double valor) {
			this.saldo -= valor;
		}

		@Override
		public double getSaldo() {
			return this.saldo;
		}
	}
	```
	
1. (Opcional) Às vezes, é interessante criarmos uma interface que herda de outras
	interfaces: essas, são chamadas subinterfaces. Essas, nada mais são do que um
	agrupamento de obrigações para a classe que a implementar.

	``` java
	public interface ContaTributavel extends Conta, Tributavel {
	}
	```

	Dessa maneira, quem for implementar essa nova interface precisa implementar todos
	os métodos herdados das suas superinterfaces (e talvez ainda novos métodos
	declarados dentro dela):

	``` java
	public class ContaCorrente implements ContaTributavel {
	  // métodos
	}

	Conta c = new ContaCorrente();
	Tributavel t = new ContaCorrente();
	```

	Repare que o código pode parecer estranho, pois a interface não declara método
	algum, só herda os métodos abstratos declarados nas outras interfaces.

	Ao mesmo tempo que uma interface pode herdar de mais de uma outra interface,
	classes só podem possuir uma classe mãe (herança simples).
	
	*Resposta*:

	Podemos criar a interface ContaTributavel, que é uma `Conta` e também é
	`Tributavel`. Como as definições dos métodos já estão nas duas interfaces
	originais, a declaração da nova fica, simplesmente:

	``` java
		public interface ContaTributavel extends Conta, Tributavel {
		}
	```

	E, então, alteramos também a ContaCorrente, que passa a implementar apenas
	essa nova interface:

	``` java
		public class ContaCorrente implements ContaTributavel {
			// restante da classe
			// exatamente igual à do exercício anterior
		}
	```

## Exercícios 12.11: Exceções
1. Na classe `Conta`, modifique o método `deposita(double x)`: Ele deve lançar uma exception
	chamada `IllegalArgumentException`, que já faz parte da biblioteca do Java, sempre que o valor
	passado como argumento for inválido (por exemplo, quando for negativo).

	``` java
	public void deposita(double valor) {
		if (valor < 0) {
			throw new IllegalArgumentException();
		} else {
			this.saldo += valor;		
		}		
	}
	```
1. Rode a aplicação, cadastre uma conta e tente depositar um valor negativo.
	O que acontece?

	*Resposta:*
	Uma `IllegalArgumentException` é lançada quando tentamos depositar um valor inválido, isto
	é, o próprio método `deposita` se defende de alguém que queira fazer algo errado.
	
1. Ao lançar a `IllegalArgumentException`, passe via construtor uma mensagem a ser exibida. Lembre
	que a `String` recebida como parâmetro é acessível depois via o método `getMessage()` herdado
	por todas as `Exceptions`.

	``` java
	public void deposita(double valor) {
		if (valor < 0) {
			throw new IllegalArgumentException("Você tentou depositar" + 
												" um valor negativo");
		} else {
			this.saldo += valor;		
		}		
	}
	```

	Rode a aplicação novamente e veja que agora a mensagem aparece na tela.
1. Faça o mesmo para o método `saca` da classe `ContaCorrente`, afinal o cliente
	também não pode sacar um valor negativo!
1. Vamos validar também que o cliente não pode sacar um valor maior
	do que o saldo disponível em conta.
	Crie sua própria `Exception`, `SaldoInsuficienteException`. Para isso, você precisa criar uma
	classe com esse nome que seja filha de `RuntimeException`.

	``` java
	public class SaldoInsuficienteException extends RuntimeException {

	}
	```

	No método `saca` da classe `ContaCorrente` vamos utilizar esta nova `Exception`:
	``` java
	@Override
	public void saca(double valor) {
		if (valor < 0) {
			throw new IllegalArgumentException("Você tentou sacar um valor negativo");
		}
		if (this.saldo < valor) {
			throw new SaldoInsuficienteException();
		}
		this.saldo -= (valor + 0.10);
	}
	```

	**Atenção:** nem sempre é interessante criarmos um novo tipo de exception! Depende do caso.
	Neste aqui, seria melhor ainda utilizarmos `IllegalArgumentException`. A boa prática diz que
	devemos preferir usar as já existentes do Java sempre que possível.
1. (opcional) Coloque um construtor na classe `SaldoInsuficienteException` que receba
	o valor	que ele tentou sacar (isto é, ele vai receber um `double valor`).

	Quando estendemos uma classe, não herdamos seus construtores, mas podemos acessá-los através
	da palavra chave `super` de dentro de um construtor. As exceções do Java possuem uma série
	de construtores úteis para poder populá-las já com uma mensagem de erro. Então vamos criar
	um construtor em `SaldoInsuficienteException` que delegue para o construtor de sua mãe. Essa
	vai guardar essa mensagem para poder mostrá-la ao ser invocado o método `getMessage`:

	

	``` java
		public class SaldoInsuficienteException extends RuntimeException {

			public SaldoInsuficienteException(double valor) {
				super("Saldo insuficiente para sacar o valor de: " + valor);
			}
		}
	```

	Dessa maneira, na hora de dar o `throw new SaldoInsuficienteException` você vai precisar passar
		esse valor como argumento:

	```java
		if (this.saldo < valor) {
			throw new SaldoInsuficienteException(valor);
		}
	```

	**Atenção:** você pode se aproveitar do Eclipse para isso: comece já passando o `valor` como
		argumento para o construtor da exception e o Eclipse vai reclamar que não existe tal construtor.
		O quick fix (`ctrl + 1`) vai sugerir que ele seja construindo, poupando-lhe tempo!

	E agora, como fica o método `saca` da classe `ContaCorrente`?
	
	*Resposta*:
	```java
	@Override
	public void saca(double valor) {
		if (valor < 0) {
			throw new IllegalArgumentException("Valor menor do que 0");
		}
		if (this.saldo < valor) {
			throw new SaldoInsuficienteException(valor);
		}
		this.saldo -= (valor + 0.10);
	}
	```

1. (opcional) Declare a classe `SaldoInsuficienteException` como filha direta de `Exception` em
	vez de `RuntimeException`. Ela passa a ser **checked**. O que isso resulta?

	Você vai precisar avisar que o seu método `saca()` `throws SaldoInsuficienteException`,
	pois ela é uma _checked_ exception. Além disso, quem chama esse método vai precisar tomar uma
	decisão entre `try-catch` ou `throws`. Faça uso do quick fix do Eclipse novamente!

	Depois, retorne a exception para _unchecked_, isto é, para ser filha de `RuntimeException`,
	pois utilizaremos ela assim em exercícios dos capítulos posteriores.
	
	*Resposta*:
	A mudança na classe `SaldoInsuficienteException` é apenas na classe mãe:

	``` java
		public class SaldoInsuficienteException extends Exception {
			//...	
		}
	```

	E, por conta disso, o método `saca` da classe `ContaCorrente` precisa avisar que pode,
	eventualmente, lançar essa exceção:

	``` java
    public void saca(double valor) throws SaldoInsuficienteException {
        if (valor < 0) {
            throw new IllegalArgumentException();
        }
        if (this.saldo < valor) {
            throw new SaldoInsuficienteException(valor);
        }
        this.saldo -= (valor + 0.10);
    }
	```

## Desafios 12.12
1. O que acontece se acabar a memória da java virtual machine?

	*Resposta:*
	O que acontece é um `java.lang.OutOfMemoryError`, que **é um** `Error` em vez de uma
	`Exception`. http://docs.oracle.com/javase/7/docs/api/java/lang/OutOfMemoryError.html

	O código para fazer esse erro é:

	``` java
		public class TestaError {
			public static void main(String[] args) {
				String[] ss = new String[Integer.MAX_VALUE];
			}
		}
	```

## Exercícios 13.5: java.lang.Object
1. Como verificar se a classe `Throwable` que é a superclasse de `Exception` também reescreve o método `toString`?

	*Resposta:*
	A maioria das classes do Java que são muito utilizadas terão seus métodos
	`equals` e `toString` reescritos convenientemente.

	Há algumas formas de verificar a sobrescrita de um método:

	* Olhar o JavaDoc: se o método estiver sobrescrito, seu novo
	comportamento estará documentado alí;
	* Abrir a classe e olhar: no Eclipse, se você tiver adicionado
	o _src.zip_ nas suas configurações, pode abrir a classe com
	**ctrl + shift + T** e olhar se o método foi sobrescrito;
	* Bom e velho Syso: outra possibilidade é criar objetos iguais, comparar
	com o `equals` e ver se funciona. Os outros métodos são, no entanto,
	bem mais eficientes.

1. Utilize-se da documentação do Java e descubra de que classe é o objeto
	referenciado pelo atributo `out` da `System`.

	Repare que, com o devido `import`, poderíamos escrever:

	``` java
	// falta a declaração da saída
	________ saida = System.out;
	saida.println("ola");
	```

	A variável `saida` precisa ser declarada de que tipo? É isso
	que você precisa descobrir. Se você digitar esse código no Eclipse, ele
	vai te sugerir um quickfix e declarará a variável para você.

	Estudaremos essa classe em um capítulo futuro.

	*Resposta:*
	A variável pública e estática `out` é do tipo `PrintStream`.
	
1. Rode a aplicação e cadastre duas contas. Na tela de detalhes de conta, verifique o que aparece na caixa de seleção de conta para transferência.
	Por que isso acontece?

	*Resposta:*
	Nesse primeiro momento, algo parecido com isso deve ser mostrado:

	```
	br.com.caelum.contas.modelo.ContaCorrente@f34a08
	```

	Porque o `toString` ainda não foi sobrescrito.
	
1. Reescreva o método `toString` da sua classe `Conta` fazendo com que uma
	mensagem mais explicativa seja devolvida. Lembre-se de aproveitar dos recursos
	do Eclipse para isto: digitando apenas o começo do nome do método a ser reescrito
	e pressionando **ctrl + espaço**, ele vai sugerir reescrever o método, poupando
	o trabalho de escrever a assinatura do método e cometer algum engano.

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

	Rode a aplicação novamente, cadastre duas contas e verifique novamente a caixa de seleção da transferência. O que aconteceu?

	*Resposta:*
	Dessa vez, o resultado foi mais agradável. Deve ter aparecido algo como:

	```
		[titular=Batman, numero=123, agencia=345]
	```
	
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

	

	Você pode usar o **ctrl + espaço** do Eclipse para escrever o esqueleto do
		método `equals`, basta digitar dentro da classe `equ` e pressionar
		**ctrl + espaço**.

	Rode a aplicação e tente adicionar duas contas com o mesmo número e agência. O que acontece?

## Exercícios 13.7: java.lang.String
1. Queremos que as contas apresentadas na caixa de seleção da transferência apareçam com o nome do titular em maiúsculas. Para fazer isso vamos alterar o método `toString` da classe `Conta`. Utilize o método `toUpperCase` da `String` para isso.

	*Resposta:*
	``` java
      @Override
      public String toString() {
	        return "[titular=" + titular.toUpperCase() + ", numero="
              + numero + ", agencia=" + agencia + "]";
	    }
	```
	
1. Após alterarmos o método `toString`, aconteceu alguma mudança com o nome do titular que é apresentado na lista de contas? Por que?

	*Resposta:*
	Não mudou nada pois os métodos da `String` sempre retornam uma nova `String` mantendo o titular da conta inalterado.
	
1. Teste os exemplos desse capítulo, para ver que uma `String` é imutável.
	
	*Resposta:*
	Exemplos de teste:

	``` java
	public class TestaString {

		public static void main(String[] args) {
			String s = "fj11";
			s.replaceAll("1", "2");
			System.out.println(s);
		}

	}
	```

	Como fazer para ele imprimir fj22?
	*Resposta*:	
	``` java
	public class TestaString {
		public static void main(String[] args) {
			String s = "fj11";
			String outra = s.replaceAll("1", "2");
			System.out.println(s);
			System.out.println(outra);
		}
	}
	```
	
1. Como fazer para saber se uma `String` se encontra dentro de outra?
	E para tirar os espaços em branco das pontas de uma `String`? E para saber
	se uma `String` está vazia? E para saber quantos caracteres
	tem uma `String`?

	Tome como hábito sempre pesquisar o JavaDoc! Conhecer a API, aos
	poucos, é fundamental para que você não precise reescrever a roda!
	
	Abra a página da documentação da classe String da versão do Java que você
	utiliza. http://docs.oracle.com/javase/7/docs/api/java/lang/String.html

	*Resposta:*
	Os exemplos dessa questão são:

	* `contains`: devolve true se a `String` contem a sequência de
	caracteres passada;
	* `trim`: devolve uma nova `String` sem caracteres brancos do início
	e do fim;
	* `isEmpty`: devolve true se a `String` está vazia. Surgiu no Java 6;
	* `length`: devolve a quantidade de caracteres da `String`.
	
1. (opcional) Escreva um método que usa os métodos `charAt` e `length` de uma
	`String` para imprimir a mesma caractere a caractere, com cada caractere em
	uma linha diferente.

	*Resposta:*
	``` java
		public void imprimeLetraPorLetra(String texto) {
			for (int i = 0; i < texto.length(); i++) {
				System.out.println(texto.charAt(i));
			}
		}
	```
	
1. (opcional) Reescreva o método do exercício anterior, mas modificando ele para que
	imprima a `String` de trás para a frente e em uma linha só. Teste-a para
	_"Socorram-me, subi no ônibus em Marrocos"_ e _"anotaram a data da maratona"_.

	

	*Resposta:*
	``` java
		public void inverte(String texto) {
			for (int i = texto.length() - 1; i >= 0; i--) {
				System.out.print(texto.charAt(i));
			}
			System.out.println("");
		}
	```

1. (opcional) Pesquise a classe `StringBuilder` (ou StringBuffer no Java 1.4).
	Ela é mutável. Por que usá-la em vez da `String`? Quando usá-la?

	Como você poderia reescrever o método de escrever a `String` de trás para a
	frente usando um `StringBuilder`?
	*Resposta*:
	``` java
		public void inverteComStringBuilder(String texto) {
			System.out.print("\t");
			StringBuilder invertido = new StringBuilder(texto).reverse();
			System.out.println(invertido);
		}
	```

	

## Desafio 13.8
1. Converta uma `String` para um número sem usar as bibliotecas do java que já
	fazem isso. Isso é, uma `String x = "762"` deve gerar um `int i = 762`.

	Para ajudar, saiba que um `char` pode ser "transformado" em `int` com o mesmo
	valor numérico fazendo:

	``` java
		char c = '3';
		int i = c - '0'; // i vale 3! 		
	```

	Aqui estamos nos aproveitando do conhecimento da tabela unicode:
	os números de 0  a 9 estão em sequência! Você poderia usar
	o método estático `Character.getNumericValue(char)` em vez disso.

	*Resposta:*
	``` java
		public class DesafioConversaoDeNumeros {

			public static void main(String[] args) {
				String numero = "762";
				System.out.println("Imprimindo a string: " + numero);

				int resultado = converteParaInt(numero);
				System.out.println("Imprimindo o int: " + resultado);
			}

			private static int converteParaInt(String numero) {
				int resultado = 0;
				while (numero.length() > 0) {
					char algarismo = numero.charAt(0);
					resultado = resultado * 10 + (algarismo - '0');
					numero = numero.substring(1);
				}
				return resultado;
			}
		}
	```

## Exercícios 14.5: Arrays

Para consolidarmos os conceitos sobre arrays, vamos fazer alguns exercícios que não interferem em nosso projeto.

1. Crie uma classe `TestaArrays` e no método `main` crie um array de contas de tamanho 10. Em seguida, faça um laço para criar 10 contas com saldos distintos e colocá-las no array. Por exemplo, você pode utilizar o índice do laço e multiplicá-lo por 100 para gerar o saldo de cada conta:

  ``` java
    Conta[] contas = new Conta[10];

    for (int i = 0; i < contas.length; i++) {
      Conta conta = new ContaCorrente();
      conta.deposita(i * 100.0);
      // escreva o código para guardar a conta na posição i do array
    }
  ```
	*A seguir a resposta completa para este item:*

	```java
	public class TestaArrays {
		public static void main(String[] args) {
		Conta[] contas = new Conta[10];

		for (int i = 0; i < contas.length; i++) {
			Conta conta = new ContaCorrente();
			conta.deposita(i * 100.0);
			contas[i] = conta;
		}
		}
	}
	```

1. Ainda na classe `TestaArrays`, faça um outro laço para calcular e imprimir a média dos saldos de todas as contas do array.
  
	*Resposta:*
	``` java
	public class TestaArrays {
		public static void main(String[] args) {
		Conta[] contas = new Conta[10];

		for (int i = 0; i < contas.length; i++) {
			Conta conta = new ContaCorrente();
			conta.deposita(i * 100.0);
			contas[i] = conta;
		}

		double soma = 0.0;
		for (int i = 0; i < contas.length; i++) {
			soma += contas[i].getSaldo();
		}
		double media = soma / contas.length;
		System.out.println("A média dos saldos é: " + media);
		}
	}
	```
  
1. (opcional) Crie uma classe ```TestaSplit``` que reescreva uma frase com as palavras na ordem invertida. _"Socorram-me, subi no ônibus em Marrocos"_ deve retornar _"Marrocos em ônibus no subi Socorram-me,"_. Utilize o método `split` da
    `String` para te auxiliar. Esse método divide uma `String` de acordo com o separador especificado e devolve as partes em um array de `String`, por exemplo:

    ``` java
        String frase = "Uma mensagem qualquer";
        String[] palavras = frase.split(" ");

        // Agora só basta percorrer o array na ordem inversa imprimindo as palavras
    ```

	*A seguir a resposta completa para este item:*
    ``` java
    public void invertePalavrasDaFrase(String texto) {
        String[] palavras = texto.split(" ");
        for (int i = palavras.length - 1; i >= 0; i--) {
        System.out.print(palavras[i] + " ");
        }
        System.out.println("");
    }
    ```

1. (opcional) Crie uma classe `Banco` dentro do pacote `br.com.caelum.contas.modelo`
	O `Banco` deve ter um nome e um número (obrigatoriamente) e uma referência a uma
	array de `Conta` de tamanho 10, além de outros atributos que você julgar necessário.

    *Resposta:*
	``` java
  	public class Banco {
      private String nome;
      private int numero;
      private Conta[] contas;

      // outros atributos que você achar necessário

      public Banco(String nome, int numero) {
          this.nome = nome;
          this.numero = numero;
          this.contas = new ContaCorrente[10];
      }

      // getters para nome e número, não colocar os setters pois já recebemos no
      // construtor
  	}
	```
1. (opcional) A classe `Banco` deve ter um método `adiciona`, que recebe uma referência a `Conta` como argumento e guarda essa conta.

    *Resposta:*
	Você deve inserir a `Conta` em uma posição da array que esteja livre.
	Existem várias maneiras para você fazer isso: guardar um contador para indicar
	qual a próxima posição vazia ou procurar por uma posição vazia toda vez. O que
	seria mais interessante?

	Se quiser verificar qual a primeira posição vazia (nula) e adicionar nela, poderia
	ser feito algo como:

	```java
  	public void adiciona(Conta c) {
      	for(int i = 0; i < this.contas.length; i++){
          // verificar se a posição está vazia
          // adicionar no array
 	     }
  	}
	```

	É importante reparar que o método adiciona não recebe titular, agencia, saldo, etc. Essa seria uma maneira nem um pouco estruturada, muito menos orientada a objetos de se trabalhar. Você antes cria uma `Conta` e já passa a referência dela, que dentro do objeto possui titular, saldo, etc.

	*Resposta:*
	```java
    public void adiciona(Conta c) {
        for(int i = 0; i < this.contas.length; i++){
            if(this.contas[i] == null) {
                this.contas[i] = c;
                break;
            }
        }
    }
	```

1. (opcional) Crie uma classe `TestaBanco` que possuirá um método `main`. Dentro dele crie
	algumas instâncias de `Conta` e passe para o banco pelo método
	`adiciona`.
    
    *Resposta:*
	``` java
  	Banco banco = new Banco("CaelumBank", 999);
  	//	 ....
	```

	Crie algumas contas e passe como argumento para o `adiciona` do banco:

    *Resposta:*
	```java
    ContaCorrente c1 = new ContaCorrente();
    c1.setTitular("Batman");
    c1.setNumero(1);
    c1.setAgencia(1000);
    c1.deposita(100000);
    banco.adiciona(c1);

    ContaPoupanca c2 = new ContaPoupanca();
    c2.setTitular("Coringa");
    c2.setNumero(2);
    c2.setAgencia(1000);
    c2.deposita(890000);
    banco.adiciona(c2);
	```

    Você pode criar essas contas dentro de um loop e dar a cada um deles valores diferentes de depósitos:

    ``` java
    for (int i = 0; i < 5; i++) {
        ContaCorrente conta = new ContaCorrente();
        conta.setTitular("Titular " + i);
        conta.setNumero(i);
        conta.setAgencia(1000);
        conta.deposita(i * 1000);
        banco.adiciona(conta);
    }
    ```

    Repare que temos de instanciar `ContaCorrente` dentro do laço. Se a instanciação
	de `ContaCorrente` ficasse acima do laço, estaríamos adicionado cinco vezes a
	**mesma** instância de `ContaCorrente` neste `Banco` e apenas mudando seu
	depósito a cada iteração, que nesse caso não é o efeito desejado.

    **Opcional**: o método `adiciona` pode gerar uma mensagem de erro indicando quando
	o array já está cheio.

    ``` java
    public class TestaBanco {

        public static void main (String[] args) {
            Banco banco = new Banco("CaelumBank", 999);

            ContaCorrente c1 = new ContaCorrente();
            c1.setTitular("Batman");
            c1.setNumero(1);
            c1.setAgencia(1000);
            c1.deposita(100000);
            banco.adiciona(c1);

            ContaPoupanca c2 = new ContaPoupanca();
            c2.setTitular("Coringa");
            c2.setNumero(2);
            c2.setAgencia(1000);
            c2.deposita(890000);
            banco.adiciona(c2);
        }
    }
    ```

1. (opcional) Percorra o atributo `contas` da sua instância de `Banco` e imprima os
	dados de todas as suas contas. Para fazer isso, você pode criar um método
	chamado `mostraContas` dentro da classe `Banco`:

	``` java
    public void mostraContas() {
        for (int i = 0; i < this.contas.length; i++) {
            System.out.println("Conta na posição " + i);
            // preencher para mostrar outras informacoes da conta
        }
    }
	```

    Cuidado ao preencher esse método: alguns índices do seu array podem não conter
    referência para uma `Conta` construída, isto é, ainda se referirem para
    `null`. Se preferir, use o `for` novo do java 5.0.

    Aí, através do seu `main`, depois de adicionar algumas contas, basta fazer:

    ``` java
        banco.mostraContas();
    ```

    ``` java
        public void mostraContas() {
            for (int i = 0; i < this.contas.length; i++) {
                Conta conta = this.contas[i];
                if (conta != null) {
                    System.out.println("Conta na posição: " + i);
                    System.out.println("Saldo da conta: " + conta.getSaldo());
                }
            }
        }
    ```

    E, também, não esqueça de alterar a classe `TestaBanco`:

    ``` java
        public class TestaBanco {

            public static void main (String[] args) {
                // criação das contas...

                banco.mostraContas();
            }
        }
    ```
	
1. (opcional) Em vez de mostrar apenas o salário de cada funcionário, você pode
	usar o método `toString()` de cada `Conta` do seu array.
	
    *Resposta:*
	``` java
    	public void mostraContas() {
        for (int i = 0; i < this.contas.length; i++) {
            Conta conta = this.contas[i];
            if (conta != null) {
                System.out.println("Conta na posição: " + i);
                System.out.println("Dados da conta: " + conta);
            }
        }
    }
	```
	
1. (opcional) Crie um método para verificar se uma determinada `Conta` se
	encontra ou não como conta deste banco:

	``` java
  	public boolean contem(Conta conta) {
      // ...
  	}
	```

    Você vai precisar fazer um `for` em seu array e verificar se a conta
    passada como argumento se encontra dentro do array. Evite ao máximo usar números
    hard-coded, isto é, use o `.length`.
        
    ``` java
        public boolean contem(Conta conta) {
            for (int i = 0; i < this.contas.length; i++) {
                if (contas.equals(this.contas[i])) {
                    return true;
                }
            }
            return false;
        }
    ```
	
3. (opcional) Caso o array já esteja cheio no momento de adicionar uma outra conta, crie um array
    novo com uma capacidade maior e copie os valores do array atual. Isto é, vamos fazer
    a realocação dos elementos do array já que java não tem isso: um array nasce e morre
    com o mesmo length.

    **Usando o this para passar argumento**

    Dentro de um método, você pode usar a palavra `this` para referenciar a si
    mesmo e pode passar essa referência como argumento.

    ``` java
        public class Banco {

            // atributos

            public void adiciona(Conta c) {
                for(int i = 0; i < this.contas.length; i++){
                    if(this.contas[i] == null) {
                        this.contas[i] = c;
                        return;
                    }
                }
                this.aumentaArray();
            }

            public void aumentaArray() {
                int novoTamanho = this.contas.length * 2;
                Conta[] maior = new Conta[novoTamanho];
                for (int i = 0; i < this.contas.length; i++) {
                    maior[i] = this.contas[i];
                }
                this.contas = maior;
            }

            // outros métodos
        }
    ```

## Exercícios 15.6: Ordenação

Vamos ordenar o campo de **destino** da tela de detalhes da conta para que as contas
apareçam em ordem alfabética de titular.

1. Faça sua classe `Conta` implementar a interface
	`Comparable<Conta>`. Utilize o critério de ordenar pelo titular da conta.

    ``` java
    public class Conta implements Comparable<Conta> {
        ...
    }
    ```

    *Resposta:*
    Deixe o seu método `compareTo` parecido com este:

    ``` java
    public class Conta implements Comparable<Conta> {

        // ... todo o código anterior fica aqui

        public int compareTo(Conta outraConta) {
                    return this.titular.compareTo(outraConta.titular);
        }
    }
    ```
1. Queremos que as contas apareçam no campo de destino ordenadas pelo titular. Vamos
	então criar o método `ordenaLista` na classe `ManipuladorDeContas`.
	Use o `Collections.sort()` para ordenar a lista recuperada do `Evento`:

    *Resposta:*
	``` java
    public class ManipuladorDeContas {

        // outros métodos

        public void ordenaLista(Evento evento) {
            List<Conta> contas = evento.getLista("destino");
            Collections.sort(contas);
        }
    }
	```

	Rode a aplicação, adicione algumas contas e verifique se as contas aparecem ordenadas
	pelo nome do titular, **no campo destino**, na parte da transferência. Para
	ver a ordenação é necessário acessar os detalhes de uma conta.

	**Atenção especial**: repare que escrevemos um método `compareTo` em nossa
	classe e nosso código **nunca** o invoca!! Isto é muito comum. Reescrevemos
	(ou implementamos) um método e quem o invocará será um outro conjunto de classes
	(nesse caso, quem está chamando o `compareTo` é o `Collections.sort`, que o
	usa como base para o algoritmo de ordenação). Isso cria um sistema extremamente
	coeso e, ao mesmo tempo, com baixo acoplamento: a classe `Collections` nunca
	imaginou que ordenaria objetos do tipo `Conta`, mas já que
	eles são `Comparable`, o seu método `sort` está satisfeito.
1. O que teria acontecido se a classe `Conta` não implementasse
	`Comparable<Conta>` mas tivesse o método `compareTo`?

	Faça um teste: remova temporariamente a sentença
	`implements Comparable<Conta>`, não remova o método `compareTo` e
	veja o que acontece. Basta ter o método, sem assinar a interface?

    *Resposta:*
	Não basta! A interface é como um contrato e sem "assiná-lo" a existência do
	método é só uma coincidência e não dá a certeza para a JVM de que a intenção
	era mesmo assinar aquele contrato.
	
1. Como posso inverter a ordem de uma lista? Como posso embaralhar
	todos os elementos de uma lista? Como posso rotacionar os elementos
	de uma lista?

	Investigue a documentação da classe `Collections` dentro do
	pacote `java.util`.
	
    *Resposta:*
	Olhando na documentação da classe `Collections`
	(http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html),
	encontramos o método `reverse()`, que recebe uma `List` e altera a ordem
	dos seus elementos, invertendo-os.
	
1. (opcional) Crie uma nova classe `TestaLista` que cria uma `ArrayList` e
	insere novas contas com saldos aleatórios usando um laço (`for`).
	Adivinhe o nome da classe para colocar saldos aleatórios? `Random`. Do pacote
	`java.util`. Consulte sua documentação para usá-la (utilize o método
	`nextInt()` passando o número máximo a ser sorteado).
	
    *Resposta:*
	``` java
    public class TestaLista {

        public static void main(String[] args) {
            List<Conta> contas = new ArrayList<Conta>();
            Random random = new Random();

            ContaPoupanca c1 = new ContaPoupanca(random.nextInt(2000), "Caio");
            c1.deposita(random.nextInt(10000) + random.nextDouble());
            contas.add(c1);

            ContaPoupanca c2 = new ContaPoupanca(random.nextInt(2000), "Adriano");
            c2.deposita(random.nextInt(10000) + random.nextDouble());
            contas.add(c2);

            ContaPoupanca c3 = new ContaPoupanca(random.nextInt(2000), "Victor");
            c3.deposita(random.nextInt(10000) + random.nextDouble());
            contas.add(c3);
        }
    }
	```
	
1. Modifique a classe `TestaLista` para utilizar uma `LinkedList` em vez de 
	`ArrayList`:

	``` java
		List<Conta> contas = new LinkedList<Conta>();
	```

	Precisamos alterar mais algum código para
	que essa substituição funcione? Rode o programa. Alguma diferença?

	
	*Resposta:*
	Essa mudança simplesmente funciona! O legal de chamar as coleções pelas suas
	interfaces é isso: não importa a implementação. Como ambas **são uma**
	`List`, é possível trocar entre elas e continuar tratando como `List`.

	É mais uma aplicação do **polimorfismo**!
	
1. (opcional) Imprima a referência para essa lista. O `toString` de uma
	`ArrayList`/`LinkedList` é reescrito?

	``` java
		System.out.println(contas);
	```
	
    *Resposta:*
	Sim! Ele mostra os elementos da lista, entre colchetes e separados por vírgulas.

## Exercícios 15.15: Collections


1. Crie um código que insira 30 mil números numa `ArrayList` e pesquise-os.
	Vamos usar um método de `System` para cronometrar o tempo gasto:

	``` java
	public class TestaPerformance {

		public static void main(String[] args) {
			System.out.println("Iniciando...");
			Collection<Integer> teste = new ArrayList<>();
			long inicio = System.currentTimeMillis();

			int total = 30000;

			for (int i = 0; i < total; i++) {
				teste.add(i);
			}

			for (int i = 0; i < total; i++) {
				teste.contains(i);
			}

			long fim = System.currentTimeMillis();
			long tempo = fim - inicio;
			System.out.println("Tempo gasto: " + tempo);
		}
	}
	```

	Troque a `ArrayList` por um `HashSet` e verifique o tempo que vai demorar:

	``` java
		Collection<Integer> teste = new HashSet<>();
	```

	O que é mais lento? A inserção de 30 mil elementos ou as 30 mil buscas? Descubra
	computando o tempo gasto em cada `for` separadamente.

	A diferença é mais que gritante. Se você passar de 30 mil para um número maior,
	como 50 ou 100 mil, verá que isso inviabiliza por completo o uso de uma `List`,
	no caso em que queremos utilizá-la essencialmente em pesquisas.

	*Resposta:*
	No caso das listas (`ArrayList` e `LinkedList`), a inserção é bem rápida e a
	busca **muito lenta**!

	No caso dos conjuntos (`TreeSet` e `HashSet`), a inserção ainda é rápida,
	embora um pouco mais lenta do que a das listas. E a busca é **muito rápida**!
	
1. (conceitual, importante) Repare que, se você declarar a coleção e der `new`
	assim:

	``` java
		Collection<Integer> teste = new ArrayList<>();
	```

	em vez de:

	``` java
		ArrayList<Integer> teste = new ArrayList<>();
	```

	É garantido que vai ter de alterar só essa linha para substituir a implementação
	por `HashSet`. Estamos aqui usando o polimorfismo para nos proteger que
	mudanças de implementação venham nos obrigar a alterar muito código. Mais uma
	vez: _programe voltado a interface, e não à implementação_!

    *Resposta:*
	Esse é um **excelente** exemplo de bom uso de interfaces, afinal, de que importa
	como a coleção funciona? O que queremos é uma coleção qualquer, isso é suficiente
	para os nossos propósitos! Nosso código está com **baixo acoplamento**
	em relação a estrutura de dados utilizada: podemos trocá-la facilmente.

	Esse é um código extremamente elegante e flexível. Com o tempo você vai reparar
	que as pessoas tentam programar sempre se referindo a essas interfaces menos
	específicas, na medida do possível: métodos costumam receber e devolver
	`Collection`s, `List`s e `Set`s em vez de referenciar diretamente uma
	implementação. É o mesmo que ocorre com o uso de `InputStream` e
	`OutputStream`: eles são o suficiente, não há porque forçar o uso de algo mais
	específico.

	Obviamente, algumas vezes não conseguimos trabalhar dessa forma e precisamos usar
	uma interface mais específica ou mesmo nos referir ao objeto pela sua
	implementação para poder chamar alguns métodos. Por exemplo, `TreeSet` tem mais
	métodos que os definidos em `Set`, assim como `LinkedList` em relação à
	`List`.

	Dê um exemplo de um caso em que não poderíamos nos referir a uma coleção de
	elementos como `Collection`, mas necessariamente por interfaces mais
	específicas como `List` ou `Set`.

	Quando precisamos colocar a semântica de que uma coleção não pode ter
	repetição, por exemplo, precisamos de um `Set`. Se precisamos
	necessariamente de ordem, precisamos de uma `List`.

	Pense na preparação de um mochilão pela Europa. Se eu estou interessado em
	contar para meus amigos por quais países eu vou passar, a repetição não
	importa, então eu escolheria um `Set`.

	Agora, se eu quero planejar as passagens de um local a outro dessa viagem,
	não só a repetição de locais importa como, também, a ordem. Então, preciso de
	uma `List`.
	
1. Faça testes com o `Map`, como visto nesse capítulo:

	``` java
	public class TestaMapa {

		public static void main(String[] args) {
			Conta c1 = new ContaCorrente();
			c1.deposita(10000);

			Conta c2 = new ContaCorrente();
			c2.deposita(3000);

			// cria o mapa
			Map mapaDeContas = new HashMap();

			// adiciona duas chaves e seus valores
			mapaDeContas.put("diretor", c1);
			mapaDeContas.put("gerente", c2);

			// qual a conta do diretor?
			Conta contaDoDiretor = (Conta) mapaDeContas.get("diretor");
			System.out.println(contaDoDiretor.getSaldo());
		}
	}
	```

	Depois, altere o código para usar o _generics_ e não haver a necessidade do
	casting, além da garantia de que nosso mapa estará seguro em relação a tipagem
	usada.

	Você pode utilizar o _quickfix_ do Eclipse para que ele conserte isso para
	você: na linha em que você está chamando o `put`, use o `ctrl + 1`. Depois de
	mais um quickfix (descubra!) seu código deve ficar como segue:

	``` java
	// cria o mapa
	Map<String, Conta> mapaDeContas = new HashMap<>();
	```

	Que opção do `ctrl + 1` você escolheu para que ele adicionasse o _generics_
	para você?

	*Resposta:*
	Há duas opções válidas aqui:

	* podemos usar o _Add type arguments to Map_ e, depois, novamente
	_Add type arguments to HashMap_;
	* podemos escolher direto a opção _Infer generic type arguments_, que
	já fará tudo com apenas um comando.

1. (opcional) Assim como no exercício 1, crie uma comparação entre `ArrayList` e
	`LinkedList`, para ver qual é a mais rápida para se adicionar elementos na
	primeira posição (`list.add(0, elemento)`), como por exemplo:

	``` java
	public class TestaPerformanceDeAdicionarNaPrimeiraPosicao {
		public static void main(String[] args) {
			System.out.println("Iniciando...");
			long inicio = System.currentTimeMillis();

			// trocar depois por ArrayList				
			List<Integer> teste = new LinkedList<>();

			for (int i = 0; i < 30000; i++) {
				teste.add(0, i);
			}

			long fim = System.currentTimeMillis();
			double tempo = (fim - inicio) / 1000.0;
			System.out.println("Tempo gasto: " + tempo);
		}
	}
	```

	Seguindo o mesmo raciocínio, você pode ver qual é a mais rápida para se percorrer
	usando o `get(indice)` (sabemos que o correto seria utilizar o _enhanced for_
	ou o `Iterator`). Para isso, insira 30 mil elementos e depois percorra-os
	usando cada implementação de `List`.

	Perceba que aqui o nosso intuito não é que você aprenda qual é o mais rápido,
	o importante é perceber que podemos tirar proveito do polimorfismo para nos
	comprometer apenas com a interface. Depois, quando necessário, podemos
	trocar e escolher uma implementação mais adequada as nossas necessidades.

	Qual das duas listas foi mais rápida para adicionar elementos à primeira posição?

	*Resposta:*
	A `LinkedList` é bem mais rápida para fazer a inserção
	**na primeira posição** do que a `ArrayList`. Isso é uma característica dos
	algoritmos dessas listas e estudada sob o tópico de _Análise de algoritmos_
	na literatura.

	Você pode aprender mais sobre isso na apostila aberta do **CS-14**, que está
	em: http://www.caelum.com.br/apostila-java-estrutura-dados/
	
1. (opcional) Crie a classe `Banco` (caso não tenha sido criada anteriormente) no
	pacote `br.com.caelum.contas.modelo` que possui uma `List` de `Conta` chamada
	`contas`. Repare que numa lista de `Conta`, você pode colocar tanto
	`ContaCorrente` quanto `ContaPoupanca` por causa do polimorfismo.

	Crie um método `void adiciona(Conta c)`, um método `Conta pega(int x)` e
	outro `int pegaQuantidadeDeContas()`. Basta usar a sua lista e delegar essas
	chamadas para os métodos e coleções que estudamos.

	Como ficou a classe `Banco`?
	
	*Resposta:*
	``` java
		public class Banco {
			private List<Conta> contas = new ArrayList<>();;

			public void adiciona(Conta conta) {
				contas.add(conta);
			}

			public Conta pega(int posicao) {
				return contas.get(posicao);
			}

			public int getQuantidadeDeContas() {
				return contas.size();
			}
		}
	```
	
1. (opcional) No `Banco`, crie um método `Conta buscaPorTitular(String nome)`
	que procura por uma `Conta` cujo `titular` seja `equals` ao `nomeDoTitular` dado.

	Você pode implementar esse método com um `for` na sua lista de `Conta`,
	porém não tem uma performance eficiente.

	Adicionando um atributo privado do tipo `Map<String, Conta>` terá um
	impacto significativo. Toda vez que o método `adiciona(Conta c)` for
	invocado, você deve invocar `.put(c.getTitular(), c)` no seu mapa.
	Dessa maneira, quando alguém invocar o método
	`Conta buscaPorTitular(String nomeDoTitular)`,
	basta você fazer o `get` no seu mapa, passando `nomeDoTitular` como argumento!

	Note, apenas, que isso é só um exercício! Dessa forma você não poderá ter dois
	clientes com o mesmo nome nesse banco, o que sabemos que não é legal.

	Como ficaria sua classe `Banco` com esse `Map`?
	
    *Resposta:*
	``` java
		public class Banco {
			private List<Conta> contas = new ArrayList<>();
			private Map<String, Conta> indexadoPorNome = new HashMap<>();

			public void adiciona(Conta conta) {
				contas.add(conta);
				indexadoPorNome.put(conta.getTitular(), conta);
			}

			public Conta buscaPorTitular(String nomeDoTitular) {
				return indexadoPorNome.get(nomeDoTitular);
			}
		}
	```
	
1. (opcional, avançado) Crie o método `hashCode` para a sua conta, de forma que
	ele respeite o `equals` de que duas contas são `equals` quando tem o mesmo
	número e agência. Felizmente para nós, o próprio Eclipse já vem com um criador de
	`equals` e `hashCode` que os faz de forma consistente.

	Na classe `Conta`, use o `ctrl + 3` e comece a escrever _hashCode_ para
	achar a opção de gerá-los. Então, selecione os atributos `numero` e `agencia` e mande
	gerar o `hashCode` e o `equals`.

	Como ficou o código gerado?
	
    *Resposta:*
	``` java
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((agencia == null) ? 0 : agencia.hashCode());
        result = prime * result + numero;
        return result;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        Conta other = (Conta) obj;
        if (agencia == null) {
            if (other.agencia != null)
                return false;
        } else if (!agencia.equals(other.agencia))
            return false;
        if (numero != other.numero)
            return false;
        return true;
    }
	```
	
1. (opcional, avançado) Crie uma classe de teste e verifique se sua classe `Conta`
	funciona agora corretamente em um `HashSet`, isto é, que ela não guarda contas
	com número e agência repetidos. Depois, remova o método `hashCode`. Continua
	funcionando?

    *Resposta:*
	Dominar o uso e o funcionamento do `hashCode` é fundamental para o bom
	programador.
	
	Sem o `hashCode`, o critério para definir o que são contas iguais e o que
	são contas diferentes se perde e, assim, o `HashSet` não consegue garantir
	a aparição única de uma conta.

	A classe para fazer essa verificação fica mais ou menos assim.

	``` java
    public class TestaHashSetDeConta {

        public static void main(String[] args) {
            HashSet<Conta> contas = new HashSet<>();

            ContaCorrente c1 = new ContaCorrente();
            c1.setNumero(1);
            c1.setAgencia(1000);
            c1.setTitular("Batman");

            ContaCorrente c2 = new ContaCorrente();
            c2.setNumero(1);
            c2.setAgencia(1000);
            c2.setTitular("Robin");

            ContaCorrente c3 = new ContaCorrente();
            c3.setNumero(2);
            c3.setAgencia(1000);
            c3.setTitular("Coringa");

            contas.add(c1);
            contas.add(c2);
            contas.add(c3);

            System.out.println("Total de contas no HashSet: " + contas.size());
        }
    }
	```

## Desafios 15.16
1. Gere todos os números entre 1 e 1000 e ordene em ordem decrescente utilizando
	um `TreeSet`. Como ficou seu código?
	
    *Resposta:*
	``` java
		public class TestaTreeSetDecrescente {

			public static void main(String[] args) {
				TreeSet<Integer> conjunto = new TreeSet<>();
				for (int i = 1; i <= 1000; i++) {
					conjunto.add(i);
				}

				for (Integer i : conjunto.descendingSet()) {
					System.out.print(i + " ");
				}
			}
		}
	```
	
1. Gere todos os números entre 1 e 1000 e ordene em ordem decrescente utilizando um
	`ArrayList`. Como ficou seu código?
	*Resposta:*
	``` java
		public class TestaArrayListDecrescente {

			public static void main(String[] args) {
				List<Integer> lista = new ArrayList<>();
				for (int i = 1; i <= 1000; i++) {
					lista.add(i);
				}

				Collections.sort(lista);
				Collections.reverse(lista);

				for (Integer i : lista) {
					System.out.print(i + " ");
				}
			}
		}
	```


## Exercícios 16.11: Java I/O

Vamos salvar as contas cadastradas em um arquivo para não precisar ficar adicionando as
contas a todo momento.
1. Na classe `ManipuladorDeContas`, crie o método `salvaDados` que recebe um
	`Evento` de onde obteremos a lista de contas:

    *Resposta:*
	``` java
  	public void salvaDados(Evento evento){
      List<Conta> contas = evento.getLista("listaContas");
      // aqui salvaremos as contas em arquivo
  	}
	```
1. Para não colocarmos todo o código de gerenciamento de arquivos dentro da classe
	`ManipuladorDeContas`, vamos criar uma nova classe cuja responsabilidade será lidar
	com a escrita / leitura de arquivos. Crie a classe `RepositorioDeContas` dentro do
	pacote `br.com.caelum.contas` e declare o método `salva` que deverá
	receber a lista de contas a serem guardadas. Neste método você deve percorrer a lista
	de contas e salvá-las separando as informações de `tipo`, `numero`, `agencia`,
	`titular` e `saldo` com vírgulas.
	O código ficará parecido com:

    *Resposta:*
	``` java
    public class RepositorioDeContas {

        public void salva(List<Conta> contas) {
            PrintStream stream = new PrintStream("contas.txt");
            for (Conta conta : contas) {
                stream.println(conta.getTipo() + "," + conta.getNumero() + ","
                    + conta.getAgencia() + "," + conta.getTitular() + ","
                    + conta.getSaldo());
            }
            stream.close();
        }
    }
	```

	O compilador vai reclamar que você não está tratando algumas exceções (como
	`java.io.FileNotFoundException`). Utilize o devido `try`/`catch` e relance a
	exceção como `RuntimeException`. Utilize o _quick fix_ do Eclipse para facilitar
	(**ctrl + 1**).

	Vale lembrar que deixar todas as exceptions passarem despercebidas não é uma boa
	prática! Você pode usar aqui, pois estamos focando apenas no aprendizado da
	utilização do `java.io`.

	Quando trabalhamos com recursos que falam com a parte externa à nossa aplicação,
	é preciso que avisemos quando acabarmos de usar esses recursos. Por isso, é
	**importantíssimo** lembrar de fechar os canais com o exterior que abrimos utilizando
	o método `close`!
1. Voltando à classe `ManipuladorDeContas`, vamos completar o método `salvaDados`
	para que utilize a nossa nova classe `RepositorioDeContas` criada.

    *Resposta:*
	``` java
    public void salvaDados(Evento evento){
        List<Conta> contas = evento.getLista("listaContas");
        RepositorioDeContas repositorio = new RepositorioDeContas();
        repositorio.salva(contas);
    }
	```

    Rode sua aplicação, cadastre algumas contas e veja se aparece um arquivo chamado
	`contas.txt` dentro do diretório `src` de seu projeto. Talvez seja necessário dar
	um F5 nele para que o arquivo apareça.
1. (Opcional, Difícil) Vamos fazer com que além de salvar os dados em um arquivo, nossa aplicação
	também consiga carregar as informações das contas para já exibir na tela. Para que a
	aplicação funcione, é necessário que a nossa classe `ManipuladorDeContas` possua um
	método chamado `carregaDados` que devolva uma `List<Conta>`. Vamos fazer o mesmo
	que anteriormente e encapsular a lógica de carregamento dentro da classe
	`RepositorioDeContas`:

	``` java
    public List<Conta> carregaDados() {
        RepositorioDeContas repositorio = new RepositorioDeContas();
        return repositorio.carrega();
    }
	```
	
	Faça o código referente ao método `carrega` que devolve uma `List` dentro da classe
	`RepositorioDeContas` utilizando a classe `Scanner`. Para obter os valores de
	cada atributo você pode utilizar o método `split` da `String`. Lembre-se que os
	atributos das contas são carregados na seguinte ordem: `tipo`, `numero`,
	`agencia`, `titular` e `saldo`. Exemplo:

	``` java
        String linha = scanner.nextLine();
        String[] valores = linha.split(",");
        String tipo = valores[0];
	```

	Além disso, a conta deve ser instanciada de acordo com o conteúdo do `tipo` obtido. Também fique atento pois os dados lidos virão sempre lidos em forma de `String` e para alguns atributos será necessário transformar o dado nos tipos primitivos correspondentes. Por exemplo:

	``` java
  		String numeroTexto = valores[1];
  		int numero = Integer.parseInt(numeroTexto);
	```

    *A seguir a resposta completa para este item:*

    ``` java
    public List<Conta> carrega() {
            List<Conta> contas = new ArrayList<>();
            try (Scanner scanner = new Scanner(new File("contas.txt"))) {
                while (scanner.hasNextLine()) {
                    Conta conta;
                    String linha = scanner.nextLine();
                    String[] valores = linha.split(",");
                    String tipo = valores[0];
                    int numero = Integer.parseInt(valores[1]);
                    String agencia = valores[2];
                    String titular = valores[3];
                    double saldo = Double.parseDouble(valores[4]);

                    if (tipo.equals("Conta Corrente")) {
                        conta = new ContaCorrente(numero, agencia, titular, saldo);
                    } else {
                        conta = new ContaPoupanca(numero, agencia, titular, saldo);
                    }
                    contas.add(conta);
                }
            } catch (FileNotFoundException e) {
                System.out.println("Não tem arquivo ainda");
            }
            return contas;
        }
    ```

1. (opcional) A classe `Scanner` é muito poderosa! Consulte seu javadoc
	para saber sobre o `delimiter` e os outros métodos `next`.
1. (opcional) Crie uma classe `TestaInteger` e vamos fazer comparações com Integers dentro do
	`main`:

	``` java
	Integer x1 = new Integer(10);
	Integer x2 = new Integer(10);

	if (x1 == x2) {
		System.out.println("igual");
	} else {
		System.out.println("diferente");
	}
	```

	

    E se testarmos com o `equals`? O que podemos concluir?

	*Resposta:*
	A conclusão é aquela mesma do capítulo de Orientação a Objeto do curso.
	Não importa que todos as informações sejam exatamente iguais: quando usamos
	o `==` estamos comparando as **variáveis**, isto é, a referência para
	objetos.

	Se demos `new` duas vezes, cada referência aponta para um objeto diferente
	e, portanto, não são iguais. Já o `equals` do `Integer`, que sobrescreve
	o do `Object`, compara o conteúdo dos objetos.
	
1. (opcional) Um `double` não está sendo suficiente para guardar a quantidade de casas
	necessárias em uma aplicação. Preciso guardar um número decimal muito grande!
	O que poderia usar?

	O `double` também tem problemas de precisão ao fazer contas, por causa de
	arredondamentos da aritmética de ponto flutuante definido pela IEEE 754:

	http://en.wikipedia.org/wiki/IEEE_754

	Ele não deve ser usado se você precisa realmente de muita precisão (casos que
	envolvam dinheiro, por exemplo).

	**Consulte a documentação**, tente adivinhar onde você pode encontrar um tipo
	que te ajudaria para resolver esses casos e veja como é intuitivo! Qual é a
	classe que resolveria esses problemas?

	Lembre-se: no Java há muito já pronto. Seja na biblioteca padrão, seja em
	bibliotecas _open source_ que você pode encontrar pela internet.

	*Resposta:*
	A classe que nos ajudará a evitar arredondamentos e a armazenar números
	decimais bem grandes é a `java.math.BigDecimal`
