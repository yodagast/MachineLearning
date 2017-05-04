### Spark基本概念

* **RDD**

RDD是Spark的基本数据类型之一，类似单机编程中的数组，可以执行map、reduce等操作。RDD分区存储在不同的机器上保持冗余，可以被并行处理。创建RDD可以：（1）普通对象转化，（2）从文件系统或者HDFS读取。

常见的RDD操作分为transformation和action: transformation对RDD进行转化，如map、filter等操作，通常是惰性的，action对RDD进行计算，如reduce、collect等。一些常见的操作包括：

Map、MapPartition\(对每个分区中的内容进行处理，每个分区中的内容以Iterator\[T\]接受\)、MapValues（对k-v中的每个values进行函数map操作）、flatMap（对每个RDD元素生产一个RDD数组类似Hive中的explode）、flastMapValues\(对于k-v中的每个values进行flatMap\)、Reduce、reduceByKey\(对k-v中相同k的values进行reduce操作，类似mysql的group函数\)。

RDD编译时类型安全，能检查出类型错误便于进行函数式编程。但由于RDD是val不变型对象，势必不断创建新的对象造成GC，其次是RDD序列化和反序列化的性能开销。（可以考虑惰性求值等方法进行编程）

RDD的容错恢复机制：lineage和checkpoint。lineage追踪RDD在DAG计算图中的依赖，并基于检查点进行恢复。具体来说Spark提供cache/persist和checkpoint。当调用cache函数时，Spark将这个数据对象保存在内存中，RDD转化为persistRDD。persist可以提供多种storageLevel的存储。如果是MEMORY\_ONLY，persist和cache方法相同。通过unpersist可以手动移除持久化数据。

checkpoint将RDD保存在HDFS中并遗忘lineagei信息，改变了RDD的DAG图信息，在下一次调用Driver程序时可以使用checkpoint中的数据。而persist\(StorageLevel.DISK\_ONLY\)只能保存RDD在硬盘中，当程序结束后blockManager会删除这些persist的数据。

* **DataFrame**：将每一行的数据存在一个schema对象中，此外DataFrame是off-heap的，直接受操作系统管理。但DataFrame不是类型安全的，如果将某个列的int类型和string进行比较，编译时期不会报错。

* **DataSet**：结合了RDD和DataFrame的优点。即可以获取每个columns的数据类型，也是编译时类型安全的。

### Spark SQL和HiveOnSpark
* HiveOnSpark 是将Hive的计算引擎由MapReduce改为Spark，提供DAG执行计划。类似的项目有HiveOnTez。

* SparkSQL 可以读取Hive表、RDD、JSON外部数据表等，使用SparkSQL进行计算。SparkSQL提供的SQL查询函数不如Hive丰富。





