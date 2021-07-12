# Apêndice - Problemas com Concorrência
_"Quem pouco pensa engana-se muito." -- Leonardo da Vinci_


## Threads acessando dados compartilhados





O uso de Threads começa a ficar interessante e complicado quando precisamos compartilhar objetos
entre várias Threads.

Imagine a seguinte situação: temos um banco com milhões de contas bancárias. Clientes sacam e
depositam dinheiro continuamente, 24 horas por dia. No primeiro dia de cada mês, o banco precisa
atualizar o saldo de todas as contas de acordo com uma taxa específica. Para isso, ele utiliza o
`AtualizadorDeContas`, que vimos anteriormente.

O `AtualizadorDeContas`, basicamente, pega cada uma das milhões de contas e chama seu
método `atualiza`. A atualização das contas é um processo demorado, que leva horas; é
inviável parar o banco por tanto tempo até que as atualizações tenham sido completas. É preciso executá-las paralelamente às atividades de depósitos e saques, normais do banco.

Ou seja, teremos várias Threads rodando simultaneamente. Em uma Thread, pegamos todas as contas e
vamos chamando o método `atualiza` de cada uma. Em outra, podemos estar sacando ou depositando
dinheiro. Estamos compartilhando objetos entre múltiplas Threads (as contas, no nosso caso).

Imagine a seguinte possibilidade (mesmo que muito remota): no exato instante em que
se está atualizando uma conta X, o cliente dono desta resolve efetuar um saque. Como
sabemos, ao trabalhar com Threads, o escalonador pode parar uma certa Thread a qualquer instante para
executar outra, e você não tem controle sobre isso.

Veja essa classe Conta:

``` java
public class Conta {		
	
	private double saldo;
		
		// outros métodos e atributos...
		
		public void atualiza(double taxa) {
			double saldoAtualizado = this.saldo * (1 + taxa);
			this.saldo = saldoAtualizado;
		}

		public void deposita(double valor) {
			double novoSaldo = this.saldo + valor;
			this.saldo = novoSaldo;
		}
}
```

Imagine uma conta com saldo de R$ 100. Um cliente entra na agência e faz um depósito de R$ 1.000. Isso dispara uma Thread no banco que chama o método `deposita()`: ele começa calculando o
`novoSaldo`, o qual passa a ser R$ 1.100 (linha 13). Só que, por algum motivo desconhecido, o
escalonador para essa Thread.

Neste exato instante, ele começa a executar uma outra Thread que chama o método `atualiza` da mesma
`Conta`, por exemplo, com taxa de 1%. Isto é, o `novoSaldo` passa a valer R$ 101
(linha 8). E, nesse momento, o escalonador troca de Threads novamente. Ele executa a linha 14
na Thread que fazia o depósito; o saldo passa a valer R$ 1.100. Acabando o método deposita, o escalonador volta
para Thread do atualiza e executa a linha 9, fazendo o saldo valer R$ 101.

Resultado: o depósito de mil reais foi totalmente ignorado e seu cliente ficará pouco feliz com isso.
Perceba que não é possível detectar esse erro, já que todo o código foi executado perfeitamente, sem
problemas. **O problema aqui foi o acesso simultâneo de duas Threads ao mesmo objeto**.

E o erro só ocorreu porque o escalonador parou nossas Threads naqueles exatos lugares. Pode ser que
nosso código fique rodando um ano sem dar problema algum e, em um belo dia, o escalonador resolve
alternar nossas Threads daquela forma. Não sabemos como o escalonador se comporta e temos de proteger
nosso código contra esse tipo de problema. Dizemos que essa classe não é _thread safe_, isto é, não
está pronta para ter uma instância utilizada entre várias Threads concorrentemente.

O que queríamos era que não fosse possível alguém atualizar a `Conta` enquanto outra pessoa está
depositando um dinheiro; mas,sim, uma Thread a qual não pudesse mexer em uma `Conta` durante o tempo em que outra
Thread está mexendo nela. Não há como impedir o escalonador de fazer tal escolha. Então, o que fazer?

## Controlando o acesso concorrente

Uma ideia seria criar uma **trava**, e, no momento em que uma Thread entrasse em um desses métodos,
ela trancaria a entrada com uma chave. Dessa maneira, mesmo sendo colocada de lado, nenhuma outra
Thread poderia entrar nesses métodos, pois a chave estaria com a outra Thread.


Essa ideia é chamada de **região crítica**. É um pedaço de código que definimos como crítico e
não pode ser executado por duas Threads ao mesmo tempo. Apenas uma por vez consegue entrar
em alguma região crítica.

Podemos fazer isso em Java. Usamos qualquer objeto como um **lock** (trava ou chave), para poder
**sincronizar** em cima desse objeto, isto é, se uma Thread entrar em um bloco que foi definido como
sincronizado por esse lock, apenas uma Thread poderá estar lá dentro ao mesmo tempo, pois a chave
estará com ela.

A palavra-chave `synchronized` dá essa característica a um bloco de código e recebe qual é o
objeto que será usado como chave. A chave só é devolvida quando a Thread que a tinha sair do bloco, seja por `return` , seja por disparo de uma exceção (ou ainda na utilização do método
`wait()`).

Queremos, então, bloquear o acesso simultâneo a uma mesma `Conta`:



``` java
public class Conta {
		
	private double saldo;
	
	// outros métodos e atributos...
		
	public void atualiza(double taxa) {
		synchronized (this) {
			double saldoAtualizado = this.saldo * (1 + taxa);
			this.saldo = saldoAtualizado;			
		}
	}
		
	public void deposita(double valor) {
		synchronized (this) {
			double novoSaldo = this.saldo + valor;
			this.saldo = novoSaldo;			
		}
	}
}
```

Observe o uso dos blocos `synchronized` dentro dos dois métodos. Eles bloqueiam uma Thread
utilizando o mesmo objeto `Conta`, o `this`.


Esses métodos são mutuamente exclusivos e só executam de maneira atômica. Threads que tentam
pegar um lock o qual já está pego ficarão em um conjunto especial esperando pela liberação do lock
(não necessariamente em uma fila).

> **Sincronizando o bloco inteiro**
>
> É comum sempre sincronizarmos um método inteiro utilizando o `this` normalmente.
>
> ``` java
> public void metodo() {
> 	synchronized (this) {
> 		// conteúdo do metodo
> 	}
> }
> ```
>
> Para esse mesmo efeito, existe uma sintaxe mais simples, na qual o `synchronized` pode ser usado como
> modificador do método:
>
> ``` java
> public synchronized void metodo() {
> 	// conteúdo do metodo
> }
> ```




> **Mais sobre locks, monitores e concorrência**
>
> Se o método for estático, será sincronizado usando o lock do objeto que representa a classe
> (`NomeDaClasse.class`).
>
> Além disso, o pacote `java.util.concurrent`, conhecido como **JUC**, entrou no Java 5.0 para
> facilitar uma série de trabalhos comuns que costumam aparecer em uma aplicação concorrente.
>
> Esse pacote ajuda até mesmo criar Threads e pool de Threads por meio dos Executors.
>
>




## Vector e Hashtable
Duas collections muito famosas são `Vector` e `Hashtable`, a diferença entre elas, suas irmãs `ArrayList`
e `HashMap` é que as aquelas primeiras são Thread Safe.

Você pode se perguntar por que não usamos sempre essas classes Thread Safe. Adquirir um lock tem
um custo, e caso um objeto não vá ser usado entre diferentes Threads, não há um porquê de usar essas classes
que consomem mais recursos. Mas nem sempre é fácil enxergar se devemos sincronizar um bloco, ou se
devemos utilizar blocos sincronizados.

Antigamente, o custo de se usar locks era altíssimo, hoje em dia, isso custa pouco para a JVM, mas
não é motivo para você sincronizar tudo sem necessidade.

## Um pouco mais...


* Você pode mudar a prioridade de cada uma de suas Threads, mas isso também é apenas uma sugestão ao escalonador.

* Existe um método `stop` nas Threads. Por que não é boa prática chamá-lo?

* Um tópico mais avançado é a utilização de `wait`, `notifiy` e `notifyAll` para que as Threads se comuniquem
sobre eventos ocorridos, indicando se podem ou não avançar de acordo com as condições.

* O pacote `java.util.concurrent` foi adicionado no Java 5 com o intuito de facilitar o trabalho na programação
concorrente. Ele tem uma série de primitivas para que você não tenha de trabalhar diretamente
com `wait` e `notify`, além de ter diversas coleções Thread Safe.



## Exercícios avançados de programação concorrente e locks

Exercícios recomendados se você já tinha algum conhecimento prévio de programação
concorrente, locks, etc.
1.  Enxerguemos o problema ao se usar uma classe que não é _thread-safe_:
	a `ArrayList` por exemplo.

	Imagine que temos um objeto o qual guarda todas as mensagens que uma aplicação
	de chat recebeu. Usemos uma `ArrayList<String>` para armazená-las.
	Nossa aplicação é _multi-thread_, então diferentes Threads vão inserir
	diferentes mensagens a serem registradas. Não importa a ordem na qual elas sejam
	guardadas, desde que elas um dia sejam!

	 Usemos a seguinte classe para adicionar as queries:

	``` java
	public class ProduzMensagens implements Runnable {
		private int comeco;
		private int fim;
		private Collection<String> mensagens;

		public ProduzMensagens(int comeco, int fim, Collection<String> mensagens) {
			this.comeco = comeco;
			this.fim = fim;
			this.mensagens = mensagens;
		}

		public void run() {
			for (int i = comeco; i < fim; i++) {
				mensagens.add("Mensagem " + i);
			}
		}
	}
	```

	 Criemos três Threads que rodem esse código e adicionem as mensagens
	na **mesma** `ArrayList`. Em outras palavras, teremos Threads compartilhando e
	acessando um mesmo objeto: é aqui onde mora o perigo.

	``` java
	public class RegistroDeMensagens {

		public static void main(String[] args) throws InterruptedException {
			Collection<String> mensagens = new ArrayList<String>();

			Thread t1 = new Thread(new ProduzMensagens(0, 10000, mensagens));
			Thread t2 = new Thread(new ProduzMensagens(10000, 20000, mensagens));
			Thread t3 = new Thread(new ProduzMensagens(20000, 30000, mensagens));

			t1.start();
			t2.start();
			t3.start();

			// Faz com que a Thread a qual roda o main aguarde o fim dessas:
			t1.join();
			t2.join();
			t3.join();

			System.out.println("Threads produtoras de mensagens finalizadas!");

			// Verifica se todas as mensagens foram guardadas:
			for (int i = 0; i < 15000; i++) {
				if (!mensagens.contains("Mensagem " + i)) {
					throw new IllegalStateException("não encontrei a mensagem: " + i);
				}
			}

			// Verifica se alguma mensagem ficou nula:
			if (mensagens.contains(null)) {
				throw new IllegalStateException("não devia ter null aqui dentro!");
			}

			System.out.println("Fim da execucao com sucesso");
		}
	}
	```

	

	Rode algumas vezes. O que acontece?
	
1. Teste o código anterior, mas usando `synchronized` ao adicionar na coleção:

	``` java
	public void run() {
		for (int i = comeco; i < fim; i++) {
			synchronized (mensagens) {
				mensagens.add("Mensagem " + i);
			}
		}
	}
	```

	

	
1. Sem usar o `synchronized`, teste com a classe `Vector`, que **é uma**
	`Collection` e _thread-safe_.

	O que mudou? Olhe o código do método `add` na classe `Vector`. O que tem de
	diferente nele?
	
1. Novamente, sem usar o `synchronized`, teste usar `HashSet` e `LinkedList`
	no lugar de `Vector`. Faça vários testes, pois as Threads vão se entrelaçar
	cada vez de uma maneira diferente, podendo ou não ter um efeito inesperado.

	
	


No capítulo de Sockets, usaremos Threads para solucionar um problema real de execuções paralelas.
