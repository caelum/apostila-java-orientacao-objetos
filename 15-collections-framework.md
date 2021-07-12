# Collections Framework
_"A amizade é um contrato segundo o qual nos comprometemos a prestar
pequenos favores para que no-los retribuam com grandes."
-- Baron de la Brede et de Montesquieu_

Ao final deste capítulo, você será capaz de:

* Utilizar arrays, lists, sets ou maps dependendo da necessidade do programa;
* Iterar e ordenar listas e coleções;
* Usar mapas para inserção e busca de objetos.


<!--@note
* Faça com que eles abram o Javadoc do java.util para eles acompanharem a documentação das classes.
* Não dar muitas explicações sobre um Hash. Explicar que é uma indexação e  _HashSet_ é
centenas de vezes mais rápido de procurar que uma _ArrayList_ (exemplo do método _contains_).
No máximo, faça analogia à indexação por primeira letra e cite que é uma tabela de espalhamento
caso alguém o conheça da faculdade.
* As pessoas têm dificuldade com generics. _Map<K,V>_ que recebe dois tipos parametrizados é pior ainda.
* Passar rapidamente pelo _Iterator_ se achar necessário. Se não, vá apenas pelo enhanced for e
explique que ele usa internamente um _Iterator_ que era a única forma antigamente.
* Comparable é um excelente exemplo de uso de interfaces. Mostre que quem criou Collections
nunca imaginou que iria comparar a classe _ContaCorrente_. Empolgue-os!
* Comentar a classe Vector, mas dizer que não se usa mais (talvez nem comentar).
* Só cite a interface Collection DEPOIS de ter apresentado Set. A ordem é: ArrayList,
LinkedList. Logo, mostre que elas implementam LIST, fale um pouco de Set e, aí
então, mostre a super interface.
-->

<!--@note
Para a galera amadurecer no uso de interfaces, vá bem devagar com a explicação.
Foi requisitado que nossa equipe modelasse a classe Banco que tem várias
Contas. Como só conhecemos array para o trabalho, usemos array mesmo.
Precisamos adicionar contas no banco e remover por índice.

``` java
class Banco {
	private Conta[] contas = new Conta[100];
	public void adiciona(Conta conta) { 
		//fazer na lousa, aumentando o tamanho se necessário
	public void remove(int indice) {
		//discutir o shifting para não só jogar referencia pra null
		//o objetivo é mostrar a dificuldade de trabalhar com arrays mesmo!
}
```

Questionar o que vai aparecer na Javadoc de nossa classe. Se precisarmos mudar
a implementação e usar algo diferente de array, haverá algum impacto para quem
estiver utilizando o Banco – usar a classe Banco em um main()?
Antes de colocarmos nossa classe em produção, foi pedido que a lista de contas
fosse devolvida para que pudesse ser mostrada em uma tabela em um aplicativo web.

Colocar getter na classe Banco.
E agora quem for usar nossa classe sabe que usamos array?
No main, o uso da classe banco:
``` java
	...
	Conta[] contas = banco.getContas();
	//usando o array na criação da tabela	
	???primeiraLinha=contas[0]; ...
```

E se decidirmos, depois, usar um tipo diferente, haverá problema?
Então, antes de mandarmos a classe para produção, pesquisemos um pouco? Apresentar o
ArrayList (sem comentar da interface ainda!). Usar fora do contexto do problema
em um main(), trabalhando apenas com String e mostrando as vantagens. Depois, mudar o uso
da array em banco para ArrayList<Conta> (já usando generics direto).
Mudar o tipo de retorno do getContas para ArrayList<Conta> e perguntar se
agora nossa classe está pronta.

Falar que mais tarde o pessoal criou alguns botões na tabela (que era só para visualização) e
começou a ter muita remoção por índice. Com muitas contas, o sistema ficou lento para essas
operações. Falar da LinkedList e da diferença entre ela e a ArrayList. E agora para mudarmos?

No main, o uso da classe banco:
``` java
	...
	ArrayList<Conta> contas = banco.getContas();
	//usando a lista na criação da tabela	
	???primeiraLinha=contas.get(0); ...
```

Falar da interface List e mudar o tipo de retorno do getContas() para List. Comentar: se tivéssemos
feito isso no começo, seria fácil a mudança (fica bem claro isso para galera).

Em turmas (MUITO?) fortes, dá para arriscar motivar também o uso de generics: mostrar fora do contexto de nossa
classe o problema de usar coleções não assinadas e perguntar se é problema para nós (o método adiciona
garante que só haverá contas em nossa coleção?).
``` java
...
List contas = banco.getContas();
contas.add("Nome");	
```

Mudar o retorno para List<Conta> (o que não impede referenciarmos pelo raw type). O problema de mostrar a
quebra de encapsulamento – especialmente se há alguma lógica no adiciona Conta c – é ficar encurralado
a falar do unmodifiableList).
-->

## Arrays são trabalhosas, utilizar estrutura de dados
Como vimos no capítulo de arrays, manipulá-las é bastante trabalhoso. Essa dificuldade
aparece em diversos momentos:


* Não podemos redimensionar uma array em Java;
* É impossível buscar diretamente por um determinado elemento cujo índice não se sabe;
* Não conseguimos saber quantas posições da array já foram populadas sem criar, para isso,
métodos auxiliares.


![ {w=50}](assets/images/collections/array1.png)

Na figura acima, você pode ver uma array que antes estava sendo completamente utilizada e depois
teve um de seus elementos removidos.

Supondo que os dados armazenados representem contas, o que acontece quando precisarmos inserir uma
nova conta no banco? Precisaremos procurar por um espaço vazio? Guardaremos em alguma estrutura de
dados externa as posições vazias? E se não houver espaço vazio? Teríamos de criar uma array maior
e copiar os dados da antiga para ela?

Há mais questões: como posso saber quantas posições estão sendo usadas na array? Terei sempre de
percorrer a array inteira para conseguir essa informação?

Além dessas dificuldades que as arrays apresentavam, faltava um conjunto robusto de classes para
suprir a necessidade de estruturas de dados básicas, como listas ligadas e tabelas de espalhamento.


Com esses e outros objetivos em mente, o comitê responsável pelo Java criou um conjunto de classes e interfaces conhecido como  **Collections Framework**, que reside no pacote `java.util` desde o Java2 1.2.

> **Collections**
>
> A **API** de **Collections** é robusta e tem diversas classes que representam estruturas de dados
> avançadas.
>
> Por exemplo, não é necessário reinventar a roda e criar uma lista ligada, mas sim utilizar aquela que
> o Java disponibiliza.

<!-- Comentário para separar quotes adjacentes. -->


## Listas: java.util.List
O primeiro dos recursos da API de `Collections` que listaremos é **lista**. Uma lista é uma coleção a qual
permite elementos duplicados e mantém uma ordenação específica entre os elementos.

Em outras palavras, você tem a garantia de que, quando percorrer a lista, os elementos serão
encontrados em uma ordem pré-determinada, definida na hora das suas inserções. Ela resolve todos os
problemas os quais levantamos em relação à array (busca, remoção, tamanho
infinito, etc.). Esse código já está pronto!

A API de `Collections` fornece a interface `java.util.List`, a qual especifica o que uma classe deve
ser capaz de fazer para ser uma lista. Há diversas implementações disponíveis, cada uma com uma forma
diferente de representar uma lista.

A implementação mais utilizada da interface `List` é a `ArrayList`, que trabalha com uma array
interna para gerar uma lista. Portanto, ela é mais rápida na pesquisa do que sua concorrente, a
`LinkedList`, a qual é mais rápida na inserção e remoção de itens nas pontas.

> **ArrayList não é uma array!**
>
> É comum confundirem uma `ArrayList` com uma array, porém ela não o é. O que ocorre é que,
> internamente, ela usa uma array como estrutura para armazenar os dados, porém esse atributo está
> propriamente encapsulado, e você não tem como acessá-lo. Repare também: você não pode usar
> `[]` com uma `ArrayList` nem acessar o atributo `length`. Não há relação!

<!-- Comentário para separar quotes adjacentes. -->


Para criar um `ArrayList`, basta chamar o construtor:

``` java
	ArrayList lista = new ArrayList();
```

<!--@note
Não mostre logo de cara que ArrayList é uma List. Acho melhor
mostrar vantagens e desvantagens em relação à velocidade com a LinkedList
e deixar os alunos em dúvida de qual usar.

Ai você diz: "para que se importar com isso agora? Vamos nos
desacoplar disso. Programar voltado à **interface**". E então apresente
a interface `List`.
-->

É sempre possível abstrair a lista a partir da interface `List`:

``` java
	List lista = new ArrayList();
```


Para criar uma lista de nomes (`String`), podemos fazer:

``` java
	List lista = new ArrayList();
	lista.add("Manoel");
	lista.add("Joaquim");
	lista.add("Maria");
```

A interface `List` tem dois métodos `add`, um que recebe o objeto a ser inserido e o coloca
no final da lista, e um segundo que permite adicionar o elemento em qualquer posição da lista.
Note que, em momento algum, dizemos qual é o tamanho da lista; podemos acrescentar quantos elementos
quisermos, pois a lista cresce conforme for necessário.

Toda lista (na verdade, toda `Collection`) trabalha do modo mais genérico possível. Isto é, não há
uma `ArrayList` específica para `String`s, outra para números, outra para datas, etc. Todos os
métodos trabalham com `Object`.

<!--@note
Aqui o instrutor tem liberdade de mostrar os métodos que achar mais interessante na lousa. Remove,
add, get, contains são bem interessantes. Cuidado com o get(), pois ele devolve object
enquanto você ainda não apresentar generics (logo a seguir).
-->


Assim, é possível criar, por exemplo, uma lista de contas-correntes:

``` java
	ContaCorrente c1 = new ContaCorrente();
	c1.deposita(100);

	ContaCorrente c2 = new ContaCorrente();
	c2.deposita(200);

	ContaCorrente c3 = new ContaCorrente();
	c3.deposita(300);

	List contas = new ArrayList();
	contas.add(c1);
	contas.add(c3);
	contas.add(c2);
```

Para saber quantos elementos há na lista, usamos o método `size()`:

``` java
	System.out.println(contas.size());
```

Há ainda um método `get(int)`, o qual recebe como argumento o índice do elemento que se quer
recuperar. Por meio dele, podemos fazer um `for` para iterar na lista de contas:

``` java
	for (int i = 0; i < contas.size(); i++) {
		contas.get(i); // código não muito útil....
	}
```

Mas como fazer para imprimir o saldo dessas contas? Podemos acessar o `getSaldo()` diretamente
após fazer `contas.get(i)`? Não podemos. Lembre-se de que toda lista trabalha sempre com `Object`.
Assim, a referência devolvida pelo `get(i)` é do tipo `Object`, sendo necessário o cast para
`ContaCorrente` se quisermos acessar o `getSaldo()`:

<!--@note
Aqui é uma boa chance para retomar a discussão de casting. Exercitar os alunos.
-->

``` java
	for (int i = 0; i < contas.size(); i++) {
		ContaCorrente cc = (ContaCorrente) contas.get(i);
		System.out.println(cc.getSaldo());
	}
	// Note que a ordem dos elementos não é alterada.
```

Há ainda outros métodos, como por exemplo o `remove()`, o qual recebe um objeto que se deseja remover da lista; e
`contains()`, que recebe um objeto como argumento e devolve `true` ou `false`, indicando se o
elemento está ou não na lista.

<!--@note
* Você pode perguntar aos alunos o que é comum eles quererem fazer com
uma array/lista.

* É uma excelente oportunidade de demonstrar seu conhecimento: eles perguntam, e você escreve na
lousa o metodo correspondente.

* É fácil induzir para que eles o motivem a mostrar indexOf, set, contains, remove(Object),
remove(int), removeAll, addAll, etc. até retainAll e toArray, dependendo da turma.

* Não deixe de dar o exemplo com o contains na lousa! Ele será usado no exercício.
Além do mais, pergunte a eles como acham que o contains funciona. Normalmente,
alguém irá perceber e dizer que ele procurará se tem um elemento `equals`, que
foi passado como argumento! (Vale lembrar que isso não é contrato da interface,
tanto que IdentityHashMap procura por ==, mas ninguém nem vai perguntar isso).
-->

A interface `List` e algumas classes que a implementam podem ser vistas no diagrama a
seguir:

![ {w=75}](assets/images/collections/list.png)

> **Acesso aleatório e percorrendo listas com get**
>
> Algumas listas, como a `ArrayList`, têm acesso aleatório aos seus elementos: a busca por um
> elemento em uma determinada posição é feita de maneira imediata, sem que a lista inteira seja
> percorrida (que chamamos de acesso sequencial).
>
> Nesse caso, o acesso por meio do método `get(int)` é muito rápido. Caso contrário,
> percorrer uma lista usando um `for` como esse que acabamos de ver pode ser desastroso. Ao
> percorrermos uma lista, devemos usar **sempre** um `Iterator` ou `enhanced for`, como veremos.

<!-- Comentário para separar quotes adjacentes. -->


Uma lista é uma excelente alternativa a uma array comum, já que temos todos os benefícios de arrays
sem a necessidade de tomar cuidado com remoções, falta de espaço, etc.

A outra implementação muito usada, a `LinkedList`, fornece métodos adicionais para obter e remover
o primeiro e último elemento da lista. Ela também tem o funcionamento interno diferente,
o que pode impactar performance, como veremos durante os exercícios no final do capítulo.

> **Vector**
>
> Outra implementação é a tradicional classe `Vector`, presente desde o Java 1.0, que foi adaptada
> para uso com o framework de Collections por meio da inclusão de novos métodos.
>
> Ela deve ser escolhida cautelosamente, pois lida de uma maneira diferente com processos correndo em
> paralelo e terá um custo adicional em relação à `ArrayList` quando não houver acesso simultâneo aos dados.

<!-- Comentário para separar quotes adjacentes.-->


## Listas no Java 5 e Java 7 com Generics
Em qualquer lista, é possível colocar qualquer `Object`. Com isso, é possível misturar objetos:

``` java
	ContaCorrente cc = new ContaCorrente();
	
	List lista = new ArrayList();
	lista.add("Uma string");
	lista.add(cc);
	...
```

Mas e depois, na hora de recuperar esses objetos? Como o método `get` devolve um `Object`,
precisamos fazer o cast. Mas, tendo uma lista com vários objetos de tipos diferentes, isso pode não ser
tão simples.

Geralmente, não nos interessa uma lista com vários tipos de objetos misturados; no dia a dia, usamos
listas como aquela de contas-correntes. No Java 5.0, podemos usar o recurso de Generics para
restringir as listas a um determinado tipo de objetos (e não qualquer `Object`):

``` java
	List<ContaCorrente> contas = new ArrayList<ContaCorrente>();
	contas.add(c1);
	contas.add(c3);
	contas.add(c2);
```

Repare no uso de um parâmetro ao lado de `List` e `ArrayList`: ele indica que nossa lista foi
criada para trabalhar exclusivamente com objetos do tipo `ContaCorrente`. Isso nos traz uma
segurança em tempo de compilação:

``` java
	contas.add("uma string"); // Isso não compila mais!!
```

O uso de Generics também elimina a necessidade de casting, uma vez que todos os objetos
inseridos na lista serão, seguramente, do tipo `ContaCorrente`:

``` java
	for(int i = 0; i < contas.size(); i++) {
		ContaCorrente cc = contas.get(i); // sem casting!
		System.out.println(cc.getSaldo());
	}
```

A partir do Java 7, se você instancia um tipo genérico na mesma linha de sua declaração, não
é necessário passar os tipos novamente, basta usar `new ArrayList<>()`. É conhecido como
_operador diamante_:

``` java
	List<ContaCorrente> contas = new ArrayList<>();
```

## A importância das interfaces nas coleções

<!--@note
* Importantíssimo frisar a elegância do design das collections!
* Volte a falar de como o Tributável nos ajudou, como Connection
é legal e já é um preparo para Comparable.
* Interface versus implementação novamente.
* Eles verão no exercício como isso ajudará em performance, apesar
de não ser única vantagem, mas isso enche os olhos dos alunos!
-->

Vale ressaltar a importância do uso da interface `List`: quando desenvolvemos,
procuramos sempre nos referir a ela, e não às implementações específicas. Por exemplo,
se temos um método que buscará uma série de contas no banco de dados, poderíamos
fazer assim:

``` java
class Agencia {
	public ArrayList<Conta> buscaTodasContas() {
		ArrayList<Conta> contas = new ArrayList<>();

		// Para cada conta do banco de dados, contas.add
		
		return contas;
	}
}
```

Porém, para que precisamos retornar a referência específica a uma `ArrayList`?
Para que ser tão específico? Dessa maneira, o dia em que optarmos por devolver
uma `LinkedList` em vez de `ArrayList`, as pessoas que estão usando o método
`buscaTodasContas` poderão ter problemas, pois estavam fazendo referência
a uma `ArrayList`. O ideal é sempre trabalhar com a interface mais genérica possível:

``` java
class Agencia {

	// modificação apenas no retorno:
	public List<Conta> buscaTodasContas() {
		ArrayList<Conta> contas = new ArrayList<>();

		// Para cada conta do banco de dados, contas.add
		
		return contas;
	}
}
```

É o mesmo caso de preferir referenciar aos objetos com `InputStream` como fizemos
no capítulo passado.

<!--@note
Esse momento é bastante importante. É fundamental para o aprendizado dos alunos
que eles saiam do FJ-11 com a certeza de que o uso de interface desacopla bastante
os seus códigos . Eles verão mais disso a seguir, com Comparable.
-->

Assim como no retorno, é boa prática trabalhar com a interface em
todos os lugares possíveis: métodos que precisam receber uma lista
de objetos têm `List` como parâmetro em vez de uma
implementação em específico, como `ArrayList`, deixando o método
mais flexível:

``` java
class Agencia {

	public void atualizaContas(List<Conta> contas) {
		// ...
	}
}
```

<!--@note
Aqui seria melhor receber List<? extends Conta>, porém entrar na discussão
do wildcard no FJ-11 é loucura.
-->

Também declaramos atributos como `List`
em vez de nos comprometer como uma ou outra implementação. Dessa
forma, obtemos um **baixo acoplamento**: podemos trocar a implementação,
já que estamos programando para a interface! Por exemplo:

``` java
class Empresa {

	private List<Funcionario> empregados = new ArrayList<>();

	// ...
}
```

## Ordenação: Collections.sort

Vimos anteriormente que as listas são percorridas de maneira pré-determinada de
acordo com a inclusão dos itens. Mas, muitas vezes, queremos percorrer a nossa
lista de maneira ordenada.

A classe `Collections` fornece um método estático `sort`, que recebe um `List`
como argumento e o ordena por ordem crescente. Por exemplo:

``` java
   List<String> lista = new ArrayList<>();
   lista.add("Sérgio");
   lista.add("Paulo");
   lista.add("Guilherme");

   // Repare que o toString de ArrayList foi sobrescrito:
   System.out.println(lista); 

   Collections.sort(lista);

   System.out.println(lista);
```

 

Ao testar o exemplo acima, você observará que, primeiro, a lista é impressa na
ordem de inserção e, depois de invocar o `sort`, ela é impressa em ordem alfabética.

Mas toda lista em Java pode ser de qualquer tipo de objeto, por exemplo,
`ContaCorrente`. E se quisermos ordenar uma lista de `ContaCorrente`? Em que
ordem a classe `Collections` ordenará? Pelo saldo? Pelo nome do correntista?

``` java
	ContaCorrente c1 = new ContaCorrente();
	c1.deposita(500);

	ContaCorrente c2 = new ContaCorrente();
	c2.deposita(200);

	ContaCorrente c3 = new ContaCorrente();
	c3.deposita(150);

	List<ContaCorrente> contas = new ArrayList<>();
	contas.add(c1);
	contas.add(c3);
	contas.add(c2);

	Collections.sort(contas); // qual seria o critério para esta ordenação?
```

Sempre que falamos em ordenação, precisamos pensar em um **critério de ordenação**,
uma forma de determinar qual elemento vem antes de qual. É necessário instruir
o `sort` sobre como **comparar** nossas `ContaCorrente` a fim de determinar
uma ordem na lista. Para isso, o método `sort` necessita que todos seus objetos
da lista sejam **comparáveis** e tenham um método que se compara com outra
`ContaCorrente`. Como é que o método `sort` terá a garantia de que a sua
classe tem esse método? Isso será feito, novamente, por meio de um contrato, ou seja, de uma interface!

<!--@note
Aqui é bem importante fazê-los raciocinarem e chegarem à conclusão de usar uma interface.
Você deve mostrar o código para ordenar a `List<ContaCorrente>` e, então, perguntar como
comparar duas contas. Depois de decidido que será por meio de um método, deve-se perguntar
"e como o autor do `Collections.sort` vai saber o nome e assinatura do metodo que deve
invocar dos seus objetos?".
-->



Façamos com que os elementos da nossa coleção implementem a interface
`java.lang.Comparable`, que define o método `int compareTo(Object)`. Esse
método deve retornar: **zero**, se o objeto comparado for **igual** àquele objeto;
um número **negativo**, se aquele objeto for **menor** que o objeto dado; e um
número **positivo**, se aquele objeto for **maior** que o objeto dado.

Para ordenar as `ContaCorrente`s por saldo, basta implementar o `Comparable`:

``` java
    public class ContaCorrente extends Conta 
    						implements Comparable<ContaCorrente> {

	    // ... todo o código anterior fica aqui

	    public int compareTo(ContaCorrente outra) {
	      if (this.saldo < outra.saldo) {
	        return -1;
	      }

	      if (this.saldo > outra.saldo) {
	        return 1;
	      }

	      return 0;
	    }
    }
```

Com o código anterior, nossa classe tornou-se "**comparável**": dados dois objetos da classe,
conseguimos dizer se um objeto é maior, menor ou igual ao outro, segundo algum critério por nós
definido. No nosso caso, a comparação será feita com base no saldo da conta.

Repare que o critério de ordenação é totalmente aberto, definido pelo programador. Se quisermos
ordenar por outro atributo (ou até por uma combinação de atributos), basta modificar a implementação
do método `compareTo` na classe.

Quando chamarmos o método `sort` de `Collections`, ele saberá como fazer a ordenação
da lista pois usará o critério que definimos no método `compareTo`.

> **Outra implementação...**
>
> O que acha da implementação abaixo?
>
> ``` java
> 		public int compareTo(Conta outra) {
> 			return Integer.compare(this.getNumero(), outra.getNumero());
> 		}
> ```

<!-- Comentário para separar quotes adjacentes. -->


Mas e o exemplo anterior com uma lista de Strings? Por que a ordenação funcionou, naquele caso, sem
precisarmos fazer nada? Simples: quem escreveu a classe `String` (lembre-se de que ela é uma classe
como qualquer outra) implementou a interface `Comparable` e o método `compareTo` para `String`s,
fazendo comparação em ordem alfabética (consulte a documentação da classe `String` e veja o método
`compareTo` lá). O mesmo acontece com outras classes, como `Integer`, `BigDecimal`, `Date`,
entre outras.


> **Outros métodos da classe Collections**
>
> A classe `Collections` apresenta uma grande quantidade de métodos estáticos úteis na manipulação de coleções.
>
>
> * `binarySearch(List, Object)`: realiza uma busca binária por determinado elemento na lista ordenada
> e retorna sua posição ou um número negativo, caso não encontrado.
>
> * `max(Collection)`: retorna o maior elemento da coleção.
>
> * `min(Collection)`: retorna o menor elemento da coleção.
>
> * `reverse(List)`: inverte a lista.
>
> * E muitos outros. Consulte a documentação para ver outros métodos.
>
>
>
> No Java 8, muitas dessas funcionalidades da `Collections` podem ser feitas por intermédio dos chamados `Streams`, que fica um pouco fora do escopo de um curso inicial de Java.
>
> Existe uma classe análoga, a `java.util.Arrays`, que faz operações similares com arrays.
>
> É importante conhecê-las para evitar escrever código já existente.

<!-- Comentário para separar quotes adjacentes. -->


## Exercícios: ordenação

Ordenaremos o campo de **destino** da tela de detalhes da conta para que as contas
apareçam em ordem alfabética de titular.
<!--@note
É muito interessante eles aprenderem sobre a API, mas, mais ainda, é que eles
consigam enxergar que todos os conceitos aprendidos até agora de OO serão
aplicados nesse exercício, em especial, o uso de interfaces, e como
isso desacopla código.
-->
1. Faça sua classe `Conta` implementar a interface
	`Comparable<Conta>`. Utilize o critério de ordenar pelo titular da conta.

	``` java
  public class Conta implements Comparable<Conta> {
      ...
  }
	```

	Deixe o seu método `compareTo` parecido com este:

	``` java
  public class Conta implements Comparable<Conta> {

      // ... todo o código anterior fica aqui

      public int compareTo(Conta outraConta) {
			    return this.titular.compareTo(outraConta.titular);
      }
  }
	```
1. Queremos que as contas apareçam no campo de destino ordenadas pelo titular. Então, criemos o método `ordenaLista` na classe `ManipuladorDeContas`.
	Use o `Collections.sort()` para ordenar a lista recuperada do `Evento`:

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
	pelo nome do titular **no campo destino**, na parte da transferência. Para
	ver a ordenação, é necessário acessar os detalhes de uma conta.

	**Atenção especial**: repare que escrevemos um método `compareTo` em nossa
	classe, e nosso código **nunca** o invoca!! Isso é muito comum. Reescrevemos
	(ou implementamos) um método, e quem o invocará será um outro conjunto de classes
	(nesse caso, quem está chamando o `compareTo` é o `Collections.sort`, que o
	usa como base para o algoritmo de ordenação). Isso cria um sistema extremamente
	coeso e, ao mesmo tempo, com baixo acoplamento: a classe `Collections` nunca
	imaginou que ordenaria objetos do tipo `Conta`, mas já que
	eles são `Comparable`, o seu método `sort` está satisfeito.
1. O que teria acontecido se a classe `Conta` não implementasse
	`Comparable<Conta>`, mas tivesse o método `compareTo`?

	Faça um teste: remova temporariamente a sentença
	`implements Comparable<Conta>`. Não remova o método `compareTo` e
	veja o que acontece. Basta ter o método sem assinar a interface?
	<!--@answer
	Não basta! A interface é como um contrato. Sem assiná-lo, a existência do
	método é só uma coincidência e não dá a certeza à JVM de que a intenção
	era mesmo assinar aquele contrato.
	-->
1. Como inverter a ordem de uma lista? Como embaralhar
	todos os elementos de uma lista? E rotacionar os elementos
	de uma lista?

	Investigue a documentação da classe `Collections` dentro do
	pacote `java.util`.
	<!--@answer
	Olhando na documentação da classe `Collections`
	(http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html),
	encontramos o método `reverse()`, que recebe uma `List` e altera a ordem
	dos seus elementos, invertendo-os.
	-->
1. (Opcional) Em uma nova classe `TestaLista`, crie
	uma `ArrayList` e
	insira novas contas com saldos aleatórios usando um laço (`for`).
	Adivinhe o nome da classe para colocar saldos aleatórios? `Random`, do pacote
	`java.util`. Consulte sua documentação para usá-la (utilize o método
	`nextInt()` passando o número máximo a ser sorteado).
	<!--@answer
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
	-->
1. Modifique a classe `TestaLista` para utilizar uma `LinkedList` em vez de 
	`ArrayList`:

	``` java
		List<Conta> contas = new LinkedList<Conta>();
	```

	Precisamos alterar mais algum código para
	que essa substituição funcione? Rode o programa. Alguma diferença?

	<!--@note
	Essa mudança é um pretexto para o exercício de performance ao final do
	capitulo.
	-->
	<!--@answer
	Essa mudança simplesmente funciona! O legal de chamar as coleções pelas suas
	interfaces é isso: não importa a implementação. Como ambas **são uma**
	`List`, é possível trocar entre elas e continuar tratando como `List`.

	É mais uma aplicação do **polimorfismo**!
	-->
1. (Opcional) Imprima a referência a essa lista. O `toString` de uma
	`ArrayList`/`LinkedList` é reescrito?

	``` java
		System.out.println(contas);
	```
	<!--@answer
	Sim! Ele mostra os elementos da lista entre colchetes e separados por vírgulas.
	-->


## Conjunto: java.util.Set

Um conjunto (`Set`) funciona de forma análoga aos conjuntos da matemática. Ele é uma coleção que
não permite elementos duplicados.

Outra característica sua fundamental é o fato de que a ordem na qual os elementos são armazenados
pode não ser aquela em que eles foram inseridos no conjunto. A interface não define como deve
ser esse comportamento. Tal ordem varia de implementação para implementação.

![ {w=60%}](assets/images/collections/conjunto.png)
![ {w=40%}](assets/images/collections/set.png)

Um conjunto é representado pela interface `Set` e tem como suas principais implementações as
classes `HashSet`, `LinkedHashSet` e `TreeSet`.

O código a seguir cria um conjunto e adiciona diversos elementos, alguns repetidos:

``` java
	Set<String> cargos = new HashSet<>();
	
	cargos.add("Gerente");
	cargos.add("Diretor");
	cargos.add("Presidente");
	cargos.add("Secretária");
	cargos.add("Funcionário");
	cargos.add("Diretor"); // repetido!

	// imprime na tela todos os elementos
	System.out.println(cargos);
```

 

Aqui o segundo `Diretor` não será adicionado, e o método `add` lhe retornará `false`.

O uso de um `Set` pode parecer desvantajoso, já que ele não armazena a ordem e não
aceita elementos repetidos. Não há métodos que trabalham com índices, como o `get(int)`, que
as listas têm. A grande vantagem do `Set` é a existência de implementações, como a `HashSet`,
que têm uma performance incomparável com as `List`s quando usadas para pesquisa (método
`contains`, por exemplo). Veremos essa enorme diferença durante os exercícios.

> **Ordem de um Set**
>
> Seria possível usar uma outra implementação de conjuntos, como um `TreeSet`, a qual insere os
> elementos de tal forma que, quando forem percorridos, eles apareçam em uma ordem definida pelo
> método de comparação entre seus elementos. Esse método é definido pela interface
> `java.lang.Comparable`. Ou, ainda, pode se passar um `Comparator` para seu construtor.
>
> Já o `LinkedHashSet` mantém a ordem de inserção dos elementos.

<!-- Comentário para separar quotes adjacentes. -->


Antes do Java 5, não podíamos utilizar generics e, por isso, usávamos o `Set` de forma que ele
trabalhava com `Object`, havendo necessidade de castings.

## Principais interfaces: java.util.Collection
As coleções têm como base a interface `Collection`, que define métodos para adicionar e remover um
elemento, além de verificar se ele está na coleção, entre outras operações, como mostra a tabela a seguir:

![ {w=90%}](assets/images/collections/metodos-collection.png)

Uma coleção pode implementar diretamente a interface `Collection`. Porém, normalmente se usa uma das
duas subinterfaces mais famosas: justamente `Set` e `List`.
	
A interface `Set`, como previamente vista, define um conjunto de elementos únicos, enquanto a interface `List`
permite elementos duplicados, além de manter a ordem na qual eles foram adicionados.

A busca em um `Set` pode ser mais rápida do que em um objeto do tipo `List`, pois diversas
implementações se utilizam de tabelas de espalhamento (_hash tables_), realizando a busca para tempo
linear (**O(1)**).


A interface `Map` faz parte do framework, mas não estende `Collection` (veremos `Map` mais
adiante).

![ {w=60%}](assets/images/collections/collection-map.png)

No Java 5, temos outra interface filha de `Collection`: a `Queue`, que define métodos de entrada
e de saída, e cujo critério será definido pela sua implementação (por exemplo LIFO, FIFO ou ainda um
heap, em que cada elemento tem sua chave de prioridade).

## Percorrendo coleções no Java 5
Como percorrer os elementos de uma coleção? Se for uma lista, podemos sempre utilizar um laço
`for`, invocando o método `get` para cada elemento. Mas e se a coleção não permitir indexação?

Por exemplo, um `Set` não tem um método para pegar o primeiro, o segundo ou o quinto elemento
do conjunto, visto que um conjunto não tem o conceito de ordem.

<!--@note
Não há problema se você já mostrou o enhanced for antes com a lista. Na apostila, mostramos
só aqui para ir devagar. A lousa ajuda e possibilita acelerar.
-->

Podemos usar o **enhanced-for** (o "foreach") do Java 5 para percorrer qualquer `Collection` sem
nos preocupar com isso. Internamente, o compilador fará com que seja usado o `Iterator` da `Collection`
dado para percorrer a coleção. Repare:

``` java
	Set<String> conjunto = new HashSet<>();
	
	conjunto.add("java");
	conjunto.add("vraptor");
	conjunto.add("scala");

	for (String palavra : conjunto) {
		System.out.println(palavra);
	}
```

 

Em que ordem os elementos serão acessados?

Em uma lista, os elementos aparecerão de acordo com o índice em que foram inseridos, isto é, em concordância com o que foi pré-determinado. Em um conjunto, a ordem depende da implementação da interface `Set`:
você, muitas vezes, não saberá ao certo em que ordem os objetos serão percorridos.

<!--@note
Você pode fazer a analogia de uma sacola e de uma fila. Numa fila, você sabe a ordem
e pode perguntar: "quem é o terceiro da fila?", já, numa sacola, não faz sentido
perguntar: "qual é o terceiro livro dentro dessa sacola?".
-->

Por que o `Set` é, então, tão importante e usado?

Para perceber se um item já existe em uma lista, é muito mais rápido usar algumas implementações de `Set`
do que um `List`, e os `TreeSets` já vêm ordenados de acordo com as características que desejarmos!
Sempre considere usar um `Set` se não houver a necessidade de guardar os elementos em determinada
ordem e buscá-los por meio de um índice.

No Eclipse, você pode escrever `foreach` e dar **Ctrl + espaço**, que ele gerará
o esqueleto desse enhanced for! Muito útil!

## Para saber mais: iterando sobre coleções com java.util.Iterator
Antes do Java 5 introduzir o novo enhanced-for, iterações em coleções eram feitas com o `Iterator`.
Toda coleção fornece acesso a um _iterator_, um objeto o qual implementa a interface `Iterator`, que
conhece internamente a coleção e dá acesso a todos os seus elementos, como a figura abaixo mostra:

![ {w=65%}](assets/images/collections/iterator.png)

Ainda hoje (depois do Java 5), podemos usar o `Iterator`,
mas o mais comum é usar o enhanced-for. E, na verdade, o enhanced-for é apenas um açúcar sintático que
usa iterator por trás dos panos.


Primeiro, criamos um `Iterator` que entra na coleção. A cada chamada do método `next`,
o `Iterator` retorna o próximo objeto do conjunto. Um `iterator` pode ser obtido com
o método `iterator()` de `Collection`, por exemplo, em uma lista de `String`:

``` java
	Iterator<String> i = lista.iterator();
```

A interface `Iterator` tem dois métodos principais: `hasNext()` (com retorno booleano), indica
se ainda existe um elemento a ser percorrido; `next()`, retorna o próximo objeto.

Voltando ao exemplo do conjunto de `String`s, percorramos o conjunto:

``` java
	Set<String> conjunto = new HashSet<>();
	conjunto.add("item 1");
	conjunto.add("item 2");
	conjunto.add("item 3");

	// retorna o iterator
	Iterator<String> i = conjunto.iterator();
	while (i.hasNext()) {
		// recebe a palavra
		String palavra = i.next();
		System.out.println(palavra);
	}	
```

 

O `while` anterior só termina quando todos os elementos do conjunto forem percorridos, isto é,
quando o método `hasNext` mencionar que não existem mais itens.

> **ListIterator**
>
> Uma lista fornece, além de acesso a um `Iterator`, um `ListIterator`, que oferece recursos
> adicionais, específicos para listas.
>
> Usando o `ListIterator`, você pode, por exemplo, adicionar um elemento à lista ou voltar ao
> elemento que foi iterado anteriormente.

<!-- Comentário para separar quotes adjacentes. -->


> **Usar Iterator em vez do enhanced-for?**
>
> O `Iterator` pode, sim, ainda ser útil. Além de iterar na coleção, como faz o
> enhanced-for, o `Iterator` consegue remover elementos da coleção durante a iteração de uma forma
> elegante por meio do método `remove`.

<!-- Comentário para separar quotes adjacentes. -->


<!--@note
Esse box é por causa do `ConcurrentModificationException`:

http://blog.caelum.com.br/concurrentmodificationexception-e-os-fail-fast-iterators/
-->

## Mapas - java.util.Map
Muitas vezes, queremos buscar rapidamente um objeto a partir de alguma informação sobre ele. Um exemplo
seria obter todos os dados do carro a partir de sua placa. Poderíamos utilizar uma lista para
isso e percorrer todos os seus elementos, mas pode ser péssimo para a performance até para
listas não muito grandes. Aqui entra o mapa.

Um mapa é composto por um conjunto de associações entre um objeto-chave e um objeto-valor.
É equivalente ao conceito de dicionário, usado em várias linguagens. Algumas linguagens, como
Perl ou PHP, têm um suporte mais direto a mapas, também chamados de matrizes/arrays
associativas.

<!--@note
Use na lousa o exemplo em uma pseudo linguagem:

cpfs["maria"] = 28848546811
cpfs["joaquim"] = 66666666666
cpfs["manoel"] = 333333331

Separe bem os lados Chave e o lado Valor. Outro exemplo bom é o `.ini` do visual basic e o
regedit do windows.
-->

`java.util.Map` é um mapa, pois é possível usá-lo para mapear uma chave a um valor, por exemplo:
mapeie o valor "caelum" à chave "empresa", ou então, o valor "Vergueiro" à chave "rua".
Semelhante a associações de palavras que podemos fazer em um dicionário.

![ {w=70%}](assets/images/collections/mapa.png)

O método `put(Object, Object)` da interface `Map` recebe a chave e o valor de uma nova
associação. Para saber o que está associado a um determinado objeto-chave, passa-se esse objeto no
método `get(Object)`. Sem dúvida, essas são as duas operações principais e mais frequentes realizadas
sobre um mapa.

Observe o exemplo: criamos duas contas-correntes e as colocamos em um mapa, associando-as aos seus donos.

``` java
    ContaCorrente c1 = new ContaCorrente();
    c1.deposita(10000);

    ContaCorrente c2 = new ContaCorrente();
    c2.deposita(3000);

    // cria o mapa
    Map<String, ContaCorrente> mapaDeContas = new HashMap<>();

    // adiciona duas chaves e seus respectivos valores
    mapaDeContas.put("diretor", c1);
    mapaDeContas.put("gerente", c2);

    // qual a conta do diretor? (sem casting!)
    ContaCorrente contaDoDiretor = mapaDeContas.get("diretor");
    System.out.println(contaDoDiretor.getSaldo());
```

Um mapa é muito usado para indexar objetos de acordo com determinado critério
com o intuito de buscá-los rapidamente. Um mapa costuma aparecer
juntamente com outras coleções para poder realizar essas buscas!

Ele, assim como as coleções, trabalha diretamente com `Objects` (tanto na chave quanto no
valor), o que tornaria necessário o casting no momento em que recuperar elementos. Usando
os generics, como fizemos aqui, não precisamos mais do casting.




Suas principais implementações são o `HashMap`, o `TreeMap` e o `Hashtable`.

Apesar de o mapa fazer parte do framework, ele não estende a interface `Collection` por ter um
comportamento bem diferente. Porém, as coleções internas de um mapa (a de chaves e a de valores, ver
Figura 7) são acessíveis por métodos definidos na interface `Map`.

![ {w=35%}](assets/images/collections/map.png)

O método `keySet()` retorna um `Set` com as chaves daquele mapa, e o método `values()` retorna
a `Collection` com todos os valores que foram associados a alguma das chaves.

## Para saber mais: Properties

<!--@note
Se for comentar na aula, compensa mostrar o mau uso de herança nesse caso. Properties herda
de Hashtable e é um Map. Nojento porque tem um metodo put(Object,Object) que não deve ser chamado
se não for String.

Do Javadoc: "Because Properties inherits from Hashtable, the put and putAll methods can be applied to
a Properties object. Their use is strongly discouraged as they allow the caller to insert entries
whose keys or values are not Strings. The setProperty method should be used instead".
-->
Um mapa importante é a tradicional classe `Properties`, que mapeia Strings e é muito utilizada para
a configuração de aplicações.

A `Properties` tem também métodos para ler e gravar o mapeamento com base em um arquivo-texto,
facilitando muito a sua persistência.

``` java
	Properties config = new Properties();
	  
	config.setProperty("database.login", "scott");
	config.setProperty("database.password", "tiger");
	config.setProperty("database.url","jdbc:mysql:/localhost/teste");

	// muitas linhas depois...

	String login = config.getProperty("database.login");
	String password = config.getProperty("database.password");
	String url = config.getProperty("database.url");
	DriverManager.getConnection(url, login, password);
```

Repare que não houve a necessidade do casting para `String` no momento de recuperar os objetos
associados. Isso porque a classe `Properties` foi desenhada a fim de trabalhar com a
associação entre `Strings`.

## Para saber mais: Equals e HashCode
Muitas das coleções do Java guardam os objetos dentro de tabelas de hash. Essas tabelas são
utilizadas para que a pesquisa de um objeto seja feita de maneira rápida.

Como funciona? Cada objeto é "classificado" pelo seu `hashCode`, e, com isso, conseguimos espalhar
cada objeto, agrupando-os pelo `hashCode`. Quando buscamos determinado objeto, só procuraremos
entre os elementos que estão no grupo daquele `hashCode`. Dentro desse grupo, testaremos o
objeto procurado com o candidato usando `equals()`.

A fim de que isso funcione direito, o método `hashCode` de cada objeto deve retornar o mesmo valor aos
dois objetos se eles são considerados `equals`. Em outras palavras:

`a.equals(b)` implica `a.hashCode() == b.hashCode()`

Implementar `hashCode` de tal maneira que ele retorne valores diferentes a dois objetos
considerados `equals` quebra o contrato de `Object`, e isso resultará em collections que usam
espalhamento (como `HashSet`, `HashMap` e `Hashtable`), não achando objetos iguais dentro de
uma mesma coleção.

> **Equals e hashCode no Eclipse**
>
> O Eclipse é capaz de gerar uma implementação correta de equals e hashcode com base nos atributos
> que você queira comparar. Basta ir no menu Source e depois em Generate hashcode() and equals().

<!-- Comentário para separar quotes adjacentes. -->


## Para saber mais: boas práticas
As coleções do Java oferecem grande flexibilidade ao usuário. A perda de performance em relação à
utilização de arrays é irrelevante, mas deve-se tomar algumas precauções:


* Grande parte das coleções usam, internamente, uma array para armazenar os seus dados. Quando
essa array não é mais suficiente, é criada uma maior, e o conteúdo da antiga é copiado. Esse processo
pode acontecer muitas vezes caso tenha uma coleção que cresce muito. Você deve, então,
criar uma coleção já com uma capacidade grande a fim de evitar o excesso de redimensionamento.

* Evite usar coleções que guardam os elementos pela sua ordem de comparação quando não há
necessidade. Um `TreeSet` gasta computacionalmente **`O(log(n))`** para inserir (ele utiliza uma
árvore rubro-negra como implementação), enquanto o `HashSet` gasta apenas **`O(1)`**.

* Não itere sobre uma `List` utilizando um `for` de `0` até `list.size()` e usando
`get(int)` para receber os objetos. Enquanto isso parece atraente, algumas implementações da
`List` não são de acesso aleatório como a `LinkedList`, o que faz esse código ter uma péssima
performance computacional. (use `Iterator`)


## Exercícios: Collections

<!--@note
Não deixe de fazer a pergunta conceitual do exercício 2 junto com os alunos também!
Eles vão poder exercitar o polimorfismo. Você pode também perguntar se valeria
a pena referenciar a ArrayList como sendo um Object e fazê-los perceberem
que é legal sempre se referenciar o mais genérico possível, mas nem sempre
faz sentido:

Object x = new ArrayList();
-->
1. Crie um código que insira 30 mil números numa `ArrayList` e pesquise-os.
	Usemos um método de `System` para cronometrar o tempo gasto:

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

	Troque a `ArrayList` por um `HashSet` e verifique o tempo que irá demorar:

	``` java
		Collection<Integer> teste = new HashSet<>();
	```

	O que é lento? A inserção de 30 mil elementos ou as 30 mil buscas? Descubra-o
	computando o tempo gasto em cada `for` separadamente.

	A diferença é mais que gritante. Se você passar de 30 mil para um número maior,
	como 50 ou 100 mil, verá que isso inviabiliza por completo o uso de uma `List`,
	uma vez que queremos utilizá-la essencialmente em pesquisas.

	<!--@answer
	No caso das listas (`ArrayList` e `LinkedList`), a inserção é bem rápida, e a
	busca **muito lenta**!

	No caso dos conjuntos (`TreeSet` e `HashSet`), a inserção ainda é rápida,
	embora um pouco mais lenta do que a das listas. E a busca é **muito rápida**!
	-->
1. (Conceitual e importante) Repare que se você declarar a coleção e der `new`
	assim:

	``` java
		Collection<Integer> teste = new ArrayList<>();
	```

	em vez de:

	``` java
		ArrayList<Integer> teste = new ArrayList<>();
	```

	É garantido que terá de alterar só essa linha para substituir a implementação
	por `HashSet`. Estamos aqui usando o polimorfismo a fim de nos proteger se por acaso
	mudanças de implementação nos obriguem a alterar muito o código. Mais uma
	vez: _programe voltado à interface, e não à implementação_!

	Esse é um **excelente** exemplo de bom uso de interfaces, afinal de que importa
	como a coleção funciona? O que queremos é uma coleção qualquer, e isso é suficiente
	para os nossos propósitos! Nosso código está com **baixo acoplamento**
	em relação à estrutura de dados utilizada: podemos trocá-la facilmente.

	Esse é um código extremamente elegante e flexível. Com o tempo, você notará
	que as pessoas tentam programar sempre se referindo a essas interfaces menos
	específicas na medida do possível: métodos costumam receber e devolver
	`Collection`s, `List`s e `Set`s em vez de referenciar diretamente uma
	implementação. É o mesmo que ocorre com o uso de `InputStream` e
	`OutputStream`: eles são o suficiente, não há um porquê de forçar a utilização de algo mais
	específico.

	Obviamente, algumas vezes, não conseguimos trabalhar dessa forma e precisamos usar
	uma interface mais específica ou mesmo nos referir ao objeto pela sua
	implementação para poder chamar alguns métodos. Por exemplo, `TreeSet` tem mais
	métodos que os definidos em `Set`, assim como `LinkedList` em relação à
	`List`.

	Dê um exemplo de um caso em que não poderíamos nos referir a uma coleção de
	elementos como `Collection`, mas necessariamente por interfaces mais
	específicas como `List` ou `Set`.

	<!--@answer
	Quando precisamos colocar a semântica de que uma coleção não pode ter
	repetição, por exemplo, precisamos de um `Set`. Se precisamos
	necessariamente de ordem, precisamos de uma `List`.

	Pense na preparação de um mochilão pela Europa. Se eu estou interessado em
	contar para meus amigos por quais países vou passar, a repetição não
	importa, então, eu escolheria um `Set`.

	Agora, se eu quero planejar as passagens de um local a outro dessa viagem,
	não só a repetição de locais importa como também a ordem. Então, preciso de
	uma `List`.
	-->
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

	Depois altere o código para usar o _generics_ e não haver a necessidade do
	casting, além da garantia de que nosso mapa estará seguro em relação à tipagem
	usada.

	 Pode utilizar o _quickfix_ do Eclipse para ele consertar isso para
	você: na linha em que está chamando o `put`, use o `ctrl + 1`. Depois de
	mais um quickfix (descubra qual!), seu código deve ficar assim:

	``` java
	// cria o mapa
	Map<String, Conta> mapaDeContas = new HashMap<>();
	```

	Que opção do `ctrl + 1` você escolheu para que ele adicionasse o _generics_?

	<!--@answer
	Há duas opções válidas aqui:

	* Podemos usar o _Add type arguments to Map_ e depois, novamente,
	_Add type arguments to HashMap_;
	* Podemos escolher direto a opção _Infer generic type arguments_, que
	já fará tudo com apenas um comando.

	-->
1. (Opcional) Assim como no exercício 1, crie uma comparação entre `ArrayList` e
	`LinkedList` a fim de verificar qual é a mais rápida para se adicionar elementos na
	primeira posição (`list.add(0, elemento)`), por exemplo:

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

	Perceba: aqui o nosso intuito não é você aprender qual é o mais rápido,
	o importante é perceber que podemos tirar proveito do polimorfismo para nos
	comprometer apenas com a interface. Depois, quando necessário, podemos
	trocar e escolher uma implementação mais adequada às nossas necessidades.

	Qual das duas listas foi mais rápida para adicionar elementos à primeira posição?

	<!--@answer
	A `LinkedList` é bem mais rápida para fazer a inserção
	**na primeira posição** do que a `ArrayList`. Isso é uma característica dos
	algoritmos dessas listas e estudada sob o tópico de _Análise de algoritmos_
	na literatura.
	-->
1. (Opcional) Crie a classe `Banco` (caso não tenha sido criada anteriormente) no
	pacote `br.com.caelum.contas.modelo`, que tem uma `List` de `Conta` chamada
	`contas`. Repare: em uma lista de `Conta`, você pode colocar tanto
	`ContaCorrente` quanto `ContaPoupanca` por causa do polimorfismo.

	Crie três métodos: `void adiciona(Conta c)`, `Conta pega(int x)` e
	`int pegaQuantidadeDeContas()`. Basta usar a sua lista e delegar essas
	chamadas aos métodos e às coleções que estudamos.

	Como ficou a classe `Banco`?
	<!--@answer
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
	-->
1. (Opcional) No `Banco`, crie um método `Conta buscaPorTitular(String nome)`
	que procura por uma `Conta` cujo `titular` seja `equals` ao `nomeDoTitular` dado.

	Você pode implementar esse método com um `for` na sua lista de `Conta`,
	porém não tem uma performance eficiente.

	Adicionando um atributo privado do tipo `Map<String, Conta>`, haverá um
	impacto significativo. Toda vez que o método `adiciona(Conta c)` for
	invocado, você deve invocar `.put(c.getTitular(), c)` no seu mapa.
	Dessa maneira, quando alguém invocar o método
	`Conta buscaPorTitular(String nomeDoTitular)`,
	basta você fazer o `get` no seu mapa, passando `nomeDoTitular` como argumento!

	Note que isso é só um exercício! Fazendo desse jeito, você não poderá ter dois
	clientes com o mesmo nome nesse banco, o que sabemos que não é legal.

	Como ficaria sua classe `Banco` com esse `Map`?
	<!--@answer
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
	-->
1. (Opcional e avançado) Crie o método `hashCode` para a sua conta de forma que
	ele respeite o `equals`: duas contas são `equals` quando têm o mesmo
	número e agência. Felizmente para nós, o próprio Eclipse já vem com um criador de
	`equals` e `hashCode`, que os faz de forma consistente.

	Na classe `Conta`, use o `ctrl + 3` e comece a escrever _hashCode_ para
	achar a opção de gerá-los. Então, selecione os atributos `numero` e `agencia` e mande
	gerar o `hashCode` e o `equals`.

	Como ficou o código gerado?
	<!--@answer
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
	-->
1. (Opcional e avançado) Crie uma classe de teste e verifique se sua classe `Conta`
	funciona agora corretamente em um `HashSet`, isto é, se ela não guarda contas
	com número e agência repetidos. Depois, remova o método `hashCode`. Continua
	funcionando?

	Dominar o uso e o funcionamento do `hashCode` é fundamental para o bom
	programador.
	<!--@answer
	Sem o `hashCode`, o critério para definir o que são contas iguais e o que
	são contas diferentes se perde e, assim, o `HashSet` não consegue garantir
	a aparição única de uma conta.

	A classe para fazer essa verificação fica mais ou menos assim:

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
	-->


## Desafios
1. Gere todos os números entre 1 e 1000 e organize-os em ordem decrescente utilizando
	um `TreeSet`. Como ficou seu código?
	<!--@answer
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
	-->
1. Gere todos os números entre 1 e 1000 e organize-os em ordem decrescente utilizando um
	`ArrayList`. Como ficou seu código?
	<!--@answer
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
	-->


## Para saber mais: Comparators, classes anônimas, Java 8 e o lambda

<!--@note
Fique atento à configuração dos computadores ao passar esses exercícios. Há a necessidade de ter o Java 8 instalado e Eclipse corretamente configurado. Em caso de emergência, instale o Java 8 localmente para os alunos e faça-os testarem esse código em um editor simples como o gedit.
-->

E se precisarmos ordenar uma lista com outro critério de comparação? Se precisarmos alterar a própria classe e mudar seu método `compareTo`, teremos apenas uma forma de comparação por vez. Precisamos de mais!

É possível definir outros critérios de ordenação usando a interface do `java.util` chamada `Comparator`. Existe um método `sort` em `Collections` que recebe, além da `List`, um `Comparator` definindo um critério de ordenação específico. É possível ter vários `Comparator`s com critérios diferentes para usar quando for necessário.

Criaremos um `Comparator` que serve para ordenar `Strings` de acordo com seu tamanho.

``` java
class ComparadorPorTamanho implements Comparator<String> {
	public int compare(String s1, String s2) {
		if(s1.length() < s2.length())
			return -1;
		if(s2.length() < s1.length())
			return 1;
		return 0;
	}
}
```


Note: diferente de `Comparable`, o método aqui se chama `compare` e recebe dois argumentos, posto que quem o implementa não é o próprio objeto.

Podemos deixá-lo mais curto, tomando proveito do método estático auxiliar `Integer.compare`, que compara dois inteiros:

``` java
class ComparadorPorTamanho implements Comparator<String> {
	public int compare(String s1, String s2) {
		return Integer.compare(s1.length(), s2.length());
	}
}
```

Depois, dentro do nosso código, teríamos que chamar a `Collections.sort`, passando o comparador também:

``` java
   List<String> lista = new ArrayList<>();
   lista.add("Sérgio");
   lista.add("Paulo");
   lista.add("Guilherme");

   // invocando o sort passando o comparador
   ComparadorPorTamanho comparador = new ComparadorPorTamanho();
   Collections.sort(lista, comparador);

   System.out.println(lista);
```

Como a variável temporária `comparador` é utilizada apenas aí, é comum escrevermos diretamente `Collections.sort(lista, new ComparadorPorTamanho())`.

### Escrevendo um Comparator com classe anônima

Repare que a classe `ComparadorPorTamanho` é bem pequena. É comum haver a necessidade de criar vários critérios de comparação, e, muitas vezes, eles são utilizados apenas em um único ponto do nosso programa.

Há uma forma de escrever essa classe e instanciá-la em uma única instrução. Você faz isso dando `new` em `Comparator`. Mas como? Se dissemos que uma interface não pode ser instanciada? Realmente `new Comparator()` não compila. Mas compilará se você abrir chaves e implementar tudo o que é necessário. Veja o código:


``` java
   List<String> lista = new ArrayList<>();
   lista.add("Sérgio");
   lista.add("Paulo");
   lista.add("Guilherme");


   Comparator<String> comparador = new Comparator<String>() {
      public int compare(String s1, String s2) {
         return Integer.compare(s1.length(), s2.length());
      }
   };
   Collections.sort(lista, comparador);

   System.out.println(lista);
```

A sintaxe é realmente esdrúxula! Em uma única linha, nós definimos uma classe e a instanciamos! Uma classe que nem mesmo nome tem. Por esse motivo, o recurso é chamado de classe anônima. Ele aparece com certa frequência, em especial, para não precisar implementar interfaces em que o código dos métodos seria muito curto e não reutilizável.

Há ainda como diminuir mais o código, evitando a criação da variável temporária `comparador` e instanciando a interface dentro da invocação para o `sort`:


``` java
   List<String> lista = new ArrayList<>();
   lista.add("Sérgio");
   lista.add("Paulo");
   lista.add("Guilherme");

   Collections.sort(lista, new Comparator<String>() {
      public int compare(String s1, String s2) {
         return Integer.compare(s1.length(), s2.length());
      }
   });

   System.out.println(lista);
```


### Escrevendo um Comparator com lambda no Java 8

Você pode fazer o download do Java 8 aqui:

https://jdk8.java.net/download.html

A partir dessa versão do Java, há uma forma mais simples de obter esse mesmo `Comparator`. Veja:

``` java
Collections.sort(lista, (s1, s2) -> Integer.compare(s1.length(), s2.length()));
```

O código `(s1, s2) -> Integer.compare(s1.length(), l2.length())` gerará uma instância de `Comparator`, em que o `compare` devolve `Integer.compare(s1.length, l2.length)`. Até mesmo o `return` não é necessário, já que só temos uma instrução após o `->`. Esse é o recurso de lambda do Java 8.

Uma outra novidade do Java 8 é a possibilidade de declarar métodos concretos dentro de uma interface, os chamados _default methods_. Até o Java 7, não existia `sort` em listas. Colocar um novo método abstrato em uma interface pode ter consequências drásticas: todo mundo que a implementava para de compilar! Mas colocar um método default não tem esse mesmo impacto devastador, uma vez que as classes as quais implementam a interface herdam esse método. Então você pode fazer:

``` java
lista.sort((s1, s2) -> Integer.compare(s1.length(), s2.length()));
```


<!--@note
Para uma turma mais avançada, voce pode chegar até o `list.sort(Comparator.comparing(String::length))`, mas precisará explicar method reference também.

Caso você queira organizar uma lista pela ordenação definida por ela mesma, você pode invocar o `sort` dessa forma `list.sort(Comparator.naturalOrder())`.
-->

Há outros métodos nas coleções que utilizam o lambda para serem mais sucintos.

Um deles é o `forEach`. Você pode fazer `lista.forEach(s -> System.out.println(s))`.

O `removeIf` é outro deles. Por exemplo, podemos escrever `lista.removeIf(c -> c.getSaldo() < 0)`. O `removeIf` recebe como argumento um objeto que implemente a interface `Predicate`, a qual tem apenas um método, o qual recebe um element e devolve `boolean`. Por ter apenas um método abstrato, também chamamos essa interface de interface funcional. O mesmo ocorre ao invocar o `forEach`, recebendo um argumento que implementa a interface funcional `Consumer`.

### Mais? Method references, streams e collectors

Trabalhar com lambdas no Java 8 vai muito além. Há diversos detalhes e recursos que não veremos nesse primeiro curso. Caso tenha curiosidade e queira saber mais, veja no blog:

http://blog.caelum.com.br/o-minimo-que-voce-deve-saber-de-java-8/

<!--@todo Exercícios. -->
