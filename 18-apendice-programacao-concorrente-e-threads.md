# Apêndice - Programação Concorrente e Threads

_"O único lugar onde o sucesso vem antes do trabalho é no dicionário." -- Albert Einstein_

Ao final deste capítulo, você será capaz de:

* Executar tarefas simultaneamente;
* Colocar tarefas para aguardar até que um determinado evento ocorra;
* Entender o funcionamento do Garbage Collector.


<!--@note
* Você não tem controle sobre o escalonador.

* Garbage Collector: você não sabe quando ele passa.

* Não precisa passar código de syncrhonized se achar a turma fraca ou estiver atrasado,
mas é necessário demonstrar os problemas graves que podem aparecer caso duas Threads
compartilhem acesso a um mesmo objeto.

* Definir o termo Thread Safe e comparar _HashMap_ com _Hashtable_ e _ArrayList_
com _Vector_ rapidamente.
-->

## Threads
### Duas tarefas ao mesmo tempo
Em várias situações, precisamos rodar duas coisas ao mesmo tempo. Imagine um programa que gera
um relatório muito grande em PDF. É um processo demorado, e, para dar alguma satisfação ao usuário,
queremos mostrar uma barra de progresso. Desejamos, então, gerar o PDF e _ao mesmo tempo_ atualizar a
barrinha.

Pensando um pouco mais amplamente, quando usamos o computador, também fazemos várias coisas simultaneamente:
queremos navegar na internet e _ao mesmo tempo_ ouvir música.

A necessidade de se fazer várias coisas  **paralelamente** aparece com frequência na computação. Para vários programas distintos, normalmente o próprio sistema operacional
gerencia isso por meio de vários _processos_ simultâneos.

Em um programa só (um processo só), se queremos executar coisas em paralelo,
normalmente falamos de **Threads**.

### Threads em Java
Em Java, usamos a classe `Thread` do pacote `java.lang` para criarmos
_linhas de execução_ paralelas. A classe `Thread` recebe como argumento um
objeto com o código que desejamos rodar. Por exemplo, no programa de PDF e barra
de progresso:

``` java
public class GeraPDF {
	public void rodar () {
		// lógica para gerar o PDF...
	}
}

public class BarraDeProgresso {
	public void rodar () {
		// mostra barra de progresso e vai atualizando-a ...
	}
}
```

E, no método `main`, criamos os objetos e passamos para a classe `Thread`. O
método `start` é responsável por iniciar a execução da `Thread`:

``` java
public class MeuPrograma {
	public static void main (String[] args) {
		
		GeraPDF gerapdf = new GeraPDF();
		Thread threadDoPdf = new Thread(gerapdf);
		threadDoPdf.start();
		
		BarraDeProgresso barraDeProgresso = new BarraDeProgresso();
		Thread threadDaBarra = new Thread(barraDeProgresso);
		threadDaBarra.start();
		
	}
}
```

O código acima, porém, não compilará. Como a classe `Thread` sabe que deve chamar
o método `roda`? Como ela sabe qual nome de método daremos e que deve chamar
esse método especial? Falta, na verdade, um **contrato** entre as nossas classes a
serem executadas e a classe `Thread`.

<!--@note
Faça aqui uma conversa com os alunos e deixe que algum deles chegue à conclusão
que para amarrar a classe Thread à sua classe, uma interface deve ser usada.
Aí você explica que já existe a Runnable.
-->

Esse contrato existe e é feito pela _interface_ `Runnable`: devemos dizer que
nossa classe é executável e segue esse contrato. Na interface `Runnable`,
há apenas um método chamado `run`. Basta implementá-lo, assinar o contrato, e
a classe `Thread` já saberá executar nossa classe.

``` java
public class GeraPDF implements Runnable {
	public void run () {
		// Lógica para gerar o PDF...
	}
}

public class BarraDeProgresso implements Runnable {
	public void run () {
		// Mostre a barra de progresso e vai atualizando-a...
	}
}
```

A classe `Thread` recebe no construtor um objeto que **é um** `Runnable`, e
seu método `start` chama o método `run` da nossa classe. Repare que a classe
`Thread` não sabe qual é o tipo específico da nossa classe; para ela, basta saber
que a classe segue o contrato estabelecido e tem o método `run`.

É o bom uso de interfaces, contratos e polimorfismo na prática!

> **Estendendo a classe Thread**
>
> A classe `Thread` implementa `Runnable`. Então você pode criar uma subclasse
> dela e reescrever o `run` que, na classe `Thread`, não faz nada:
>
> ``` java
> public class GeraPDF extends Thread {
> 	public void run () {
> 		// ...
> 	}
> }
> ```
>
> E, como nossa classe **é uma** `Thread`, podemos usar o `start` diretamente:
>
> ``` java
> GeraPDF gera = new GeraPDF();
> gera.start();
> ```
>
> Apesar de ser um código mais simples, você está usando herança apenas por
> preguiça (herdamos um monte de métodos, mas usamos apenas o `run`), e não por
> polimorfismo, que seria a grande vantagem. Prefira implementar `Runnable` a
> herdar de `Thread`.

<!-- Comentário para separar quotes adjacentes. -->


> **Dormindo**
>
> Com o intuito de que a Thread atual durma, basta chamar o método a seguir, por exemplo, para
> dormir três segundos:
>
> ``` javaThread.sleep(3 * 1000);```

<!-- Comentário para separar quotes adjacentes. -->


## Escalonador e trocas de contexto

Veja a classe a seguir:

``` java
public class Programa implements Runnable {

	private int id;		   
	// colocar getter e setter pro atributo id

	public void run () {
		for (int i = 0; i < 10000; i++) {
		    System.out.println("Programa " + id + " valor: " + i);
		}
	}
}
```

É uma classe que implementa `Runnable` e, no método `run`, apenas imprime
dez mil números. Vamos usá-la duas vezes para criar duas Threads e imprimir os
números duas vezes simultaneamente:

<!--@note
É uma boa mostrar para os alunos como não se chama o método run diretamente,
senão seria sequencial. O start chama o run numa Thread em paralelo.
-->

``` java
public class Teste {
	public static void main(String[] args) {
		
		Programa p1 = new Programa();	
		p1.setId(1);

		Thread t1 = new Thread(p1);
		t1.start();
		
		Programa p2 = new Programa();	
		p2.setId(2);

		Thread t2 = new Thread(p2);
		t2.start();				
		 	
	}
}
```

 

Se rodarmos esse programa, qual será a saída? De um a mil e depois de um a mil?
Provavelmente não, senão seria sequencial. Ele imprimirá 0 de t1, 0 de t2, 1 de
t1, 1 de t2, 2 de t1, 2 de t2, etc.? Exatamente intercalado?

Na verdade, não sabemos exatamente qual é a saída. Rode o programa várias vezes
e observe: em cada execução, a saída é um pouco diferente.

O problema é que no computador existe apenas um processador capaz de executar
coisas. O que ocorre quando queremos executar várias coisas ao mesmo tempo, e o processador
só consegue fazer uma coisa de cada vez? Entra em cena o **escalonador de Threads**.

O escalonador (**scheduler**), sabendo que apenas uma coisa pode ser executada de
cada vez, pega todas as Threads que precisam ser executadas e faz o processador
ficar alternando a execução de cada uma delas. A ideia é executar um pouco de cada
Thread e fazer essa troca tão rapidamente que há a impressão de que as coisas
estão sendo feitas ao mesmo tempo.

O escalonador é responsável por escolher qual a próxima Thread será executada e fazer a **troca de contexto**
(context switch). Ele primeiro salva o estado da execução da Thread atual para depois poder retomar a sua execução. Aí ele restaura o estado da Thread que será executada e faz o processador continuar a execução daquela primeira.
Depois de um certo tempo, aquela Thread é tirada do processador, seu estado (o contexto) é salvo, e outra Thread
é colocada em execução. A _troca de contexto_ é justamente as operações de salvar o contexto da Thread atual
e restaurar o da Thread que será executada em seguida.

Quando fizer a troca de contexto, por quanto tempo a Thread rodará e qual será a próxima Thread a ser
executada são escolhas do escalonador. Nós não as controlamos (embora possamos dar dicas ao
escalonador). Por isso, nunca sabemos, ao certo, a ordem em que programas paralelos são executados.

Você pode pensar que é ruim não saber a ordem. Mas perceba que se a esta importa para você, se é essencial
que determinada coisa seja feita antes de outra, então não estamos falando de execuções paralelas, mas, sim,
de um programa sequencial normal (em que uma coisa é feita depois da outra, em uma sequência).

Todo esse processo é feito automaticamente pelo escalonador do Java (e, mais amplamente, pelo escalonador do
sistema operacional). Para nós, programadores das Threads, é como se as coisas estivessem sendo executadas
ao mesmo tempo.

> **E em mais de um processador?**
>
> A VM do Java e a maioria dos SOs modernos conseguem tirar proveito de sistemas com vários processadores ou
> multi-core. A diferença é que agora temos mais de um processador executando coisas e teremos, sim, execuções
> verdadeiramente concomitantes.
>
> Mas o número de processos no SO e o número de Threads paralelas costumam ser tão grandes que, mesmo com vários
> processadores, temos as trocas de contexto. A diferença é que o escalonador tem dois ou mais processadores para
> executar suas threads. Mas dificilmente haverá uma máquina que executa com mais processadores do que Threads simultâneas.

<!-- Comentário para separar quotes adjacentes. -->


## Garbage Collector


O **Garbage Collector** (coletor de lixo/lixeiro) funciona como uma `Thread` responsável
por jogar fora todos os objetos que não estão sendo referenciados por nenhum
outro objeto - seja de maneira direta, seja de maneira indireta.

Considere o código:

``` java
	Conta conta1 = new ContaCorrente();
	Conta conta2 = new ContaCorrente();
```

Até esse momento, sabemos que temos dois objetos em memória. Aqui, o _Garbage Collector_ não pode eliminar
nenhum dos objetos, pois ainda tem alguém se referindo a eles de alguma forma.

Podemos, então, executar uma linha que nos faça perder a referência a um dos dois objetos criados,
por exemplo, o seguinte código:

``` java
	conta2 = conta1;
```

Quantos objetos temos em memória?

Perdemos a referência a um dos objetos que foram criados. Esse objeto já não é mais acessível.
Temos, então, apenas um objeto em memória? Não podemos afirmar isso. Como o _Garbage Collector_
é uma Thread, você não tem garantia de quando ele
rodará. Você só sabe que, em algum momento no futuro, aquela memória será liberada.

Algumas pessoas costumam atribuir `null` a uma variável com o intuito de acelerar a passagem do
_Garbage Collector_ por aquele objeto:

``` java
	for (int i = 0; i < 100; i++) {
		List x = new ArrayList();
		// faz algumas coisas com a arraylist
		x = null;
	}
```

Isso raramente é necessário. O _Garbage Collector_ age apenas sobre objetos, nunca sobre variáveis.
Nesse caso, a variável `x` não existirá mais a cada iteração, deixando a `ArrayList` criada sem nenhuma
referência a ela.

<!--@note
Em alguns casos particulares, é interessante atribuir `null`, por exemplo, quando você tem uma
referência que é um atributo e já não vai mais usar aquele objeto.

Ou ainda no caso de você alocar um objeto muito grande e não precisar mais dele, mas, logo em
seguida, no mesmo metodo, você faz um `wait()` ou algo que demore muito. Como a stack só
limpará as variáveis locais no fim do metodo, o GC entenderá que aquele objeto grande ainda pode estar
em uso. Isso é apenas por curiosidade, obviamente não faz sentido entrar nessa profundidade.
Saiba mais em:

http://www.javaspecialists.eu/archive/Issue173.html
http://www.javaspecialists.eu/archive/Issue174.html
-->

> **System.gc()**
>
>
> Você nunca consegue forçar o Garbage Collector, mas chamando o método estático `gc` da classe
> `System`, está sugerindo que a Virtual Machine rode o Garbage Collector naquele momento.
> Se sua sugestão será aceita ou não, isso depende de JVM para JVM, e não há garantias.
> Evite o uso desse método. Você não deve basear sua aplicação em quando o Garbage Collector irá
> rodar ou não.

<!-- Comentário para separar quotes adjacentes. -->


> **Finalizer**
>
>
>
> A classe `Object` define também um método `finalize`, que você pode reescrever. Esse método
> será chamado no instante antes do Garbage Collector coletar esse objeto. Não é um destrutor,
> você não sabe em que momento ele será chamado. Algumas pessoas o utilizam para liberar recursos
> caros como conexões, Threads e recursos nativos. Isso deve ser utilizado apenas por segurança:
> o ideal é liberá-los o mais rápido possível sem depender da passagem do Garbage
> Collector.

<!-- Comentário para separar quotes adjacentes. -->



## Exercícios
1. Teste o exemplo deste capítulo para imprimir números em paralelo.

	Escreva a classe Programa:

	``` java
	public class Programa implements Runnable {

		private int id;		   
		// colocar getter e setter pro atributo id

		public void run () {
			for (int i = 0; i < 10000; i++) {
				System.out.println("Programa " + id + " valor: " + i);
			}
		}
	}
	```

	Escreva a classe de Teste:

	``` java
	public class Teste {
		public static void main(String[] args) {

			Programa p1 = new Programa();	
			p1.setId(1);

			Thread t1 = new Thread(p1);
			t1.start();

			Programa p2 = new Programa();	
			p2.setId(2);

			Thread t2 = new Thread(p2);
			t2.start();				

		}
	}
	```

	Rode várias vezes a classe `Teste` e observe os diferentes resultados em
	cada execução. O que muda?
	<!--@answer
	O ponto em que as Threads são alternadas varia (e não temos controle sobre
	isso).
	-->


## E as classes anônimas?

É comum aparecer uma classe anônima junto a uma Thread. Vimos como usá-la com o `Comparator`. Descobriremos como utilizá-la em um `Runnable`.

Considere um `Runnable` simples que só manda imprimir algo na saída padrão:

``` java
	public class Programa1 implements Runnable {
		public void run () {
			for (int i = 0; i < 10000; i++) {
				System.out.println("Programa 1 valor: " + i);
			}
		}
	}
```

No seu `main`, você faz:

``` java
		Runnable r = new Programa1();
		Thread t = new Thread(r);
		t.start();
```

Em vez de criar essa classe `Programa1`, podemos utilizar o recurso de classe anônima. Ela nos permite dar `new` numa interface, desde que implementemos seus métodos. Com isso, podemos colocar diretamente no `main`:

``` java
Runnable r = new Runnable() {
	public void run() {
		for(int i = 0; i < 10000; i++)
			System.out.println("programa 1 valor " + i);
	}
};
Thread t = new Thread(r);
t.start();
```

> **Limitações das classes anônimas**
>
> O uso de classes anônimas tem limitações. Não podemos declarar um construtor. Como estamos instanciando uma interface, então não conseguimos passar um parâmetro para ela. De que forma, então, passamos o `id` como argumento? Você pode, de dentro de uma classe anônima, acessar os atributos da classe dentro daquela que foi declarada. Também pode acessar as variáveis locais do método, desde que elas sejam `final`.

<!-- Comentário para separar quotes adjacentes. -->


### E com lambda do Java 8?

Dá para ir mais longe com o Java 8, utilizando o lambda. Como `Runnable` é uma interface funcional (contém apenas um método abstrato), ela pode ser facilmente escrita dessa forma:

``` java
		Runnable r = () -> {
			for(int i = 0; i < 10000; i++)
				System.out.println("programa 1 valor " + i);
		};
		Thread t = new Thread(r);
		t.start();
```

A sintaxe pode ser um pouco estranha. Como não há parâmetros a serem recebidos pelo método `run`, usamos o `()` para indicá-lo. Vale lembrar, mais uma vez, que, no lambda, não precisamos escrever o nome do método o qual estamos implementando, no nosso caso o `run`. Isso é possível, pois existe apenas um método abstrato na interface.

Quer deixar o código mais enxuto ainda? Podemos passar o lambda diretamente para o construtor de `Thread` sem criar uma variável temporária. E, logo em seguida, chamar o `start`:

``` java
		new Thread(() -> {
			for(int i = 0; i < 10000; i++)
				System.out.println("programa 1 valor " + i);
		}).start();
```

Obviamente o uso excessivo de lambdas e classes anônimas pode causar uma certa falta de legibilidade. Você deve lembrar que usamos esses recursos a fim de escrever códigos mais legíveis, e não apenas para poupar algumas linhas de código. Caso nossa implementação do lambda venha a ser de várias linhas, isso é um forte sinal de que deveríamos ter uma classe à parte somente para ela.
