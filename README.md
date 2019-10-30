<h1>Desafio</h1>

<h3>Qual o objetivo do comando cache em Spark?</h3>
<p>O comando cache é um mecanismo para acelerar aplicativos que acessam o mesmo Resilient Distributed Datasets (RDD) várias vezes. Existem duas chamadas de função para armazenar em cache um RDD: cache () e persist (nível: StorageLevel) . A diferença entre eles é que cache () armazenará em cache o RDD na memória, enquanto persist (nível) pode armazenar em cache na memória, no disco ou na memória fora da pilha de acordo com a estratégia de cache especificada por nível. </p>

<h3>O mesmo código implementado em Spark é normalmente mais rápido que a implementação equivalente em
MapReduce. Por quê?</h3>
<p>Spark é capaz de executar programas até 100x mais rápidos que o Hadoop MapReduce na memória ou 10x mais rápido no disco. Isso acontece porque faz o processamento na memória principal dos nós e evita as operações de E / S desnecessárias com os discos. A outra vantagem que o Spark oferece é a capacidade de encadear as tarefas mesmo no nível de programação de aplicativos sem gravar nos discos ou minimizar o número de gravações nos discos.</p>

<h3>Qual é a função do SparkContext?</h3>
<p>O SparkContext funciona como um cliente do ambiente de execução Spark. Através dele, passam-se as configurações que vão ser utilizadas na alocação de recursos, como memória e processadores, pelos executors. Também usa-se o SparkContext para criar RDDs, colocar jobs em execução, criar variáveis de broadcast e acumuladores.</p>

<h3>Explique com suas palavras o que é Resilient Distributed Datasets (RDD).</h3>
<p>RDD é uma estrutura de dados importante no Spark. Sendo uma coleção imutável de objetos distribuidos, que é divido em partições lógicas que podem ser calculadas em diferentes nós.</p>

<h3>GroupByKey é menos eficiente que reduceByKey em grandes dataset. Por quê?</h3>
<p>A agregação usando o reduzByKey executa uma operação como parâmetros em todos os elementos da mesma chave e cada partição pode obter um resultado parcial antes de passar esses dados aos executores irão calcular o resultado final, resultando em um conjunto menor de dados. Por outro lado, ao usar groupByKey, o cálculo parcial do resultado não é realizado. Assim, uma quantidade muito maior de dados é desnecessariamente transferida entre os executores criando a necessidade de gravar dados no disco e resultando em um impacto negativo muito significativo no desempenho.</p>

<h3>Explique o que o código Scala abaixo faz.</h3>
<code>val textFile = sc.textFile("hdfs://...")
val counts = textFile.flatMap(line => line.split(" "))
.map(word => (word, 1))
.reduceByKey(_ + _)
counts.saveAsTextFile("hdfs://...")</code>