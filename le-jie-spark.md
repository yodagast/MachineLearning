### Spark调优技巧
- Spark不同的配置类型，包括：（1）Spark的应用环境如配置模式（client和cluster）、master的URL、Driver的信息等；（2）运行时环境，包含的Java类库、Java虚拟机的配置等；（3）**Shuffle的策略**：map文件是否压缩，文件缓存等。（4）Spark UI的配置。（5）**压缩和序列化的配置**，通常的尽量使用官方推荐的Kryo序列化库，广播变量、shuffle过程中的数据都默认使用lz4压缩，而RDD只有序列化后才能压缩，通常使用压缩会增加性能开销。（5）**内存管理配置**：包括Spark的执行内存（execution）和存储内存(storage),是否开启offHeap，已经offHeap的大小等。（6）**动态分配**（Dynamic Allocation），如配置initialExecutors/minExecutors/maxExecutors等，注意需要shuffle.service.enabled。（7）安全控制配置；（8）**SparkSQL配置**，包括配置spark.sql.codegen，从而获取更好的表达式查询速度。（9）Spark Streaming相关配置（略）。
### Spark基本概念

**RDD** 是Spark的基本数据类型之一，类似单机编程中的数组，可以执行map、reduce等操作。RDD分区存储在不同的机器上保持冗余，可以被并行处理。创建RDD有两种方法：（1）普通对象转化，（2）从文件系统或者HDFS读取。

常见的RDD操作分为transformation和action: transformation对RDD进行转化，如map、filter等操作，transformation生成的RDD只依赖父RDD称之为narrow dependency，通常是惰性的，action对RDD进行计算，如reduce、collect，join等，如c=a.join(b)有可能产生wide dependency或ShuffleDependency。一些常见的操作包括：

Map、MapPartition\(对每个分区中的内容进行处理，每个分区中的内容以Iterator\[T\]接受\)、MapValues（对k-v中的每个values进行函数map操作）、flatMap（对每个RDD元素生产一个RDD数组类似Hive中的explode）、flastMapValues\(对于k-v中的每个values进行flatMap\)、Reduce、reduceByKey\(对k-v中相同k的values进行reduce操作，类似mysql的group函数\)。

RDD编译时类型安全，能检查出类型错误便于进行函数式编程。但由于RDD是val不变型对象，势必不断创建新的对象造成GC，其次是RDD序列化和反序列化的性能开销。（可以考虑惰性求值等方法进行编程）

RDD的容错恢复机制：lineage和checkpoint。lineage追踪RDD在DAG计算图中的依赖，并基于检查点进行恢复。具体来说Spark提供cache/persist和checkpoint。当调用cache函数时，Spark将这个数据对象保存在内存中，RDD转化为persistRDD。persist可以提供多种storageLevel的存储。如果是MEMORY\_ONLY，persist和cache方法相同。通过unpersist可以手动移除持久化数据。

checkpoint将RDD保存在HDFS中并遗忘lineage信息，改变了RDD的DAG图信息，在下一次调用Driver程序时可以使用checkpoint中的数据。而persist\(StorageLevel.DISK\_ONLY\)只能保存RDD在硬盘中，当程序结束后blockManager会删除这些persist的数据。

广播变量Broadcast是一个read-only的数据对象，可以将数据发送到每个计算节点上，便于进行join等操作。有两种类型的广播变量HttpBroadcast和TorrentBroadcast。

**DataFrame** 将每一行的数据存在一个schema对象中，此外DataFrame是off-heap的，直接受操作系统管理。但DataFrame不是类型安全的，如果将某个列的int类型和string进行比较，编译时期不会报错。

**DataSet** 结合了RDD和DataFrame的优点。即可以获取每个columns的数据类型，也是编译时类型安全的。

### SparkSQL和HiveOnSpark
* HiveOnSpark 是将Hive的计算引擎由MapReduce改为Spark，提供DAG执行计划，加快了Hive的查询速度，类似的项目有HiveOnTez。

* SparkSQL 可以读取Hive表、RDD、JSON外部数据表等，使用SparkSQL进行计算。SparkSQL提供的SQL查询函数不如Hive丰富。

### Spark和Hadoop的Shuffle比较
* hadoop的Shuffle机制是基于排序方法的。
* Spark的Shuffle机制有sort-based和hashmap两种。

### Spark内存管理
Spark内存布局分为Execution内存和Storage内存。1.5以前使用StaticMemoryManager，但这种方式不能适应不同记得计算场景。1.6以后采用UnifiedMemoryManager。
**Storage内存**，用来缓存Task数据、在Spark集群中传输（Propagation）内部数据；
**Execution内存**，用于满足Shuffle、Join、Sort、Aggregation计算过程中对内存的需求。
使用UnifiedMemoryManager可以动态伸缩。在storage和execution中抽象出soft boundary。当某一个内存区中内存用量不足的时候，可以从另一个内存区中借用。


参考资料：

关于Spark内部原理：https://github.com/JerryLead/SparkInternals

关于Spark Shuffle：http://jerryshao.me/architecture/2014/01/04/spark-shuffle-detail-investigation/


