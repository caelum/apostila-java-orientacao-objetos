# Como Aprender Java
_"Busco um instante feliz que justifique minha existência." -- Fiodór Dostoiévski_

<!--@note
Schedule estimado para o curso noturno:

Dia 1: o que são Java, controle de fluxo e variáveis.
Dia 2: orientação a objetos básica. 
Dia 3: array e modificadores.
Dia 4: herança e polimorfismo.
Dia 5: eclipse e classes abstratas.
Dia 6: interfaces e exceptions.
Dia 7: pacotes, Javadoc e pacote padrão.
Dia 8: java io e collections (início).
Dia 9: collections (fim).
Dia 10: threads e sockets.

Alguns instrutores preferem passar mais rapidamente java io e collections. Então,
dá tempo para estender-se em classes abstratas e interfaces.
-->


<!--@note
Aprender orientação a objetos é um choque, pois muda o paradigma e a forma de pensar. É tudo
muito novo, desafiador e empolgante.

Com o tempo, acostumamo-nos com a ideia, e tudo passa a ser trivial e óbvio. Não haveria
como ser diferente. Para fazer com que os alunos entendam a orientação a objetos e se
apaixonem pela ideia (assim como foi conosco), precisamos lembrar sempre do nosso começo, quando tivemos os primeiros estalos.

Em suma, para dar o FJ-11, precisamos nos _apaixonar de novo_ pela orientação a objetos.

=== Objetivos do curso

* Que o aluno saia apto a aprender a utilizar qualquer biblioteca por meio de sua
documentação (exemplos: JFreeChart, log4j e JasperReports). Para isso, o apêndice de socket
e de JFreeChart, em que aprendemos a fazer algo difícil. Percebe-se que o complicado
são os conceitos, e a API é trivial.

* Salientar que o uso de alguns conceitos, como exceções, interfaces e classes abstratas,
somente são entendidos por completo depois de um tempo de prática com modelagem.

* Mostrar que decorar API não é importante.

* 75% da carga horária é voltada aos conceitos, somente 25% à API (a partir do java.io).
Isso mostra a facilidade de usar o Java. Mas, antes, há bastante chão.

=== Ideias que devem ser repetidas diversas vezes durante o curso:

* Objetos são *sempre* acessados por referência.
* Desenhar uma referência apontando para um objeto.
* Programa voltado à interface, e não à implementação [GoF].
* Encapsulamento: suas classes devem esconder como realizam o trabalho.
* Polimorfismo é a chave para o sucesso, e interface é o modo mais elegante de usá-lo.
* Desenhar o UML das classes apenas como suporte, sem dar formalidades.
* Java tem uma estrutura simples, mas precisamos de muitos conceitos para entendê-la. 
* Muita coisa já está pronta. Devemos aprender a procurar nas APIs do Java e nas open source
antes de criar nossa biblioteca, e-mail, gráfico, log, etc.


------------------------
Fazer uma apresentação do curso dizendo o que vamos aprender. É importante limitar
os escopos do curso, mas deixar brechas para perguntas como: "e a parte de banco
de dados?". Valer-se disso para fazer um leve marketing dos outros cursos.

É importante explicar que um dos intuitos do curso é proporcionar autonomia para
que possam caminhar com as próprias pernas.

Destacar a importância dos desafios e pedir para que tentem estudar em casa. Sabemos
que todos andam ocupados e trabalham, mas é legal sugerir que tentem ler no ônibus
ou em qualquer momento vago. É importante destacar que os desafios escondem tópicos
interessantes da computação os quais vão além do Java.

==== Apresentação

Uma das partes mais importantes. Pois é, neste ponto, os alunos têm que se sentir tranquilos
e animados em relação ao curso.

Apresentar:

Nome do curso;
Colocar o e-mail na lousa;
Resumo sobre a história da empresa (irmãos Silveira). Lembrar de destacar que o curso é
focado no mercado, diferente dos cursos da Oracle/Sun, por exemplo (não falar direto isso);
Nome e minicurrículo do instrutor - Importante focar nos projetos interessantes;
Pedir para que cada aluno se apresente dizendo o nome e o motivo que o leva a fazer o curso;
Isso é importante para fazer futuros comentários dirigidos a cada interesse.

Novamente, a apresentação é o cartão de visitas para o curso! Há de ser bem natural e falar 
claramente a fim de que os alunos se sintam confiantes.
-->

## O que é realmente importante?

Muitos livros, ao passar dos capítulos, mencionam todos os detalhes da linguagem
junto aos seus princípios básicos. Isso acaba criando muita confusão, especialmente
porque o estudante não consegue distinguir exatamente o que é primordial aprender no início
daquilo que pode ser estudado mais adiante.

Indagações como se uma classe abstrata deve ou não ter ao menos um método abstrato, se o if só
aceita argumentos booleanos e todos os detalhes sobre classes internas realmente não
devem se tornar preocupações para aquele cujo objetivo primário é aprender Java.
Esse tipo de informação será adquirido com o tempo e não é necessário no início.

Neste curso, separamos essas informações em quadros especiais, já que são extras.
Ou, então,  citamo-las num exercício e deixamos para o leitor pesquisá-las se
for de seu interesse.

Por fim, falta mencionar algo sobre a prática que deve ser tratada seriamente: todos os exercícios
são muito importantes, e os desafios podem ser feitos quando o curso terminar. De qualquer maneira,
recomendamos aos alunos que estudem em casa e pratiquem bastante código e variações. 

> **O curso**
>
> Para aqueles que estão fazendo o curso Java e Orientação a Objetos, recomendamos estudar em
> casa aquilo que foi visto durante a aula, tentando resolver os exercícios opcionais e
> os desafios apresentados.

<!-- Comentário para separar quotes adjacentes. -->


## Sobre os exercícios
Os exercícios do curso variam de práticos até pesquisas na internet ou mesmo consultas sobre assuntos
avançados em determinados tópicos para incitar a curiosidade do aprendiz na tecnologia.

Existe também, em determinados capítulos, uma série de desafios que foca mais no problema
computacional que na linguagem. Porém, é uma excelente forma de treinar a sintaxe e,
principalmente, familiarizar o aluno com a biblioteca padrão Java, além de proporcionar
um ganho na velocidade de desenvolvimento.

No capítulo 23, há possibilidades de respostas para os exercícios e desafios.

## Tirando dúvidas e indo além

Para tirar dúvidas dos exercícios ou de Java em geral, recomendamos o fórum
do GUJ (http://www.guj.com.br/), no qual sua dúvida será respondida prontamente.
O GUJ foi fundado por desenvolvedores da Caelum e, hoje, conta com mais de um milhão
de mensagens.

Fora isso, sinta-se à vontade para entrar em contato com seu instrutor e tirar todas
as dúvidas que surgirem durante o curso.

Se o que você está buscando são livros de apoio, sugerimos a editora Casa do Código:

http://www.casadocodigo.com.br

A Caelum fornece muitos outros cursos Java, com destaque para o FJ-21, que apresenta a aplicação
do Java na web.

http://www.caelum.com.br/

Há também cursos online que vão ajudá-lo a ir além, interagindo bastante
com os instrutores da Alura:

http://www.alura.com.br/
