# Semantix
Desafio Tecnico Semantix

# Questão 1: Qual o objetivo do comando cache em Spark?
Este comando tem como principal objetivo melhorar a eficiência do código, pois o mesmo permite que os resultados possam ser armazenados e reutilizados repetidamente no formato RDD. Logo, quando os dados gravados estão na memória facilitando o acesso e uso ao mesmos, pois não terão que ser carregados novamente quando reutilizados.

# Questão 2: O mesmo código implementado em Spark é normalmente mais rápido que a implementação equivalente em MapReduce. Por quê?
Spark e MapReduce são os mais populares frameworks para computação de cluster e utilização de análises em Big Data.

MapReduce é um dos mais antigos e conhecidos frameworks, o mesmo segue o modelo de programação funcional, executando a sincronização explícita através de etapas. Tal função é amplamente conhecida e utilizada, porém possuiu limitações, geralmente, em algoritmos iterativos, que realizam a leitura dos dados uma vez, mas utilizam os mesmos n vezes. Em outras palavras, muitos processamentos são feitos cmuitas vezes com os mesmos dados representando uma sobrecarga significativa.

Spark é um framework para clusterização e análise de dados em grande escala, o qual executa o processamento em memória, ou seja, sem utilização de escrita e leitura em disco rígido, sendo assim superior aos motores de buscas baseados em disco como o MapReduce. 
Com o objetivo de superar as limitações do MapReduce o Spark utiliza RDDs (Resilient Distributed Datasets), o qual grava os dados em memorioa cache. Assim, uma vez que as RDDs estão em memória, os algoritmos interagem de forma mais eficiente com os mesmos quando comparados com o processamento em MapReduce.

# Questão 3: Qual é a função do SparkContext?
SparkContext executa a função principal do usuário e as várias operações paralelas no nós de trablaho. O SparkContext se conecta a vários tipos de gerenciadores de cluster. Tais gerenciadores de cluster incluem o Apache Mesos, o Apache Hadoop YARN ou o gerenciador de cluster do Spark. Quando conectado, o Spark adquire executores em nós de trabalhado no cluster, que são processos que executam cálculos e armazenam dados para o seu aplicativo. Em seguida, ele envia o código do seu aplicativo para os executores. Por fim, o SparkContext envia tarefas para serem realizadas pelos executores.

# Questão 4: Explique com suas palavras o que é Resilient Distributed Datasets (RDD).
RDD (Resilient Distributed Dataset) é o conceito central do framework Spark, o qual mantêm as características essenciais do outro framework MapReduce (Tolerância a falhas, transparência de localização de dados e escalabilidade), porém o mesmo é como se fosse uma tabela que consegue armazenar em diferentes partições qualquer tipo de dados, ajudando na reorganização computacional e otimização no processamento dos dados em grande escala, diferente do MapReduce.
O RDD pode somente  ser criado através de funções determinísticas (map, filter, join, groupBy) executadas em outros RDDs ou meios de armazenamentos estáveis.Em outras palavras, RDDs suportam dois tipos de operações: Transformações (map, filter, join, union, etc) e Ações (reduce, count, first, etc).


# Questão 5: GroupByKey é menos eficiente que reduceByKey em grandes dataset. Por quê?

ReduceByKey e groupByKey são funções que  produzem os mesmos resultados. Porém, o groupByKey transfere todo o Dataset pela rede, enquanto o ReduceByKey calcula somas locais em cada partição para cada chave e posteriormente combinas em somais maiores após o shuffle.

# Questão 6: Explique o que o código Scala abaixo faz.
# val textFile = sc.textFile("hdfs://...") 
 . Lê os dados, armazezando em HDFS em strings RDD com o nome de textFile

# val counts = textFile.flatMap(line => line.split(" "))
# .map(word => (word, 1))
# .reduceByKey(_ + _)
            
.flatMap: pegamos os RDD das linhas e transformamos em RDD de palavras
.map: transformamos os RDD de palavras in RDD de tuplas ('palavra',1)
.reduceByKey: Para cada palavra reduzimos os valores somando todas, tendo um RDD de tuplas do tipo: ('palavra', número de ocorrências).

# counts.saveAsTextFile("hdfs://...")
O resultado do contador é gravado em um HDFS.



