
### Scala

1. **函数式编程**
将函数作为第一类对象（和普通的数据类型、对象一样可以赋值、作为参数、当做返回值），支持lambda表达式、惰性计算、闭包、表达式等特性。

2. **面向表达式编程**
在Scala中，任何代码块、函数、对象除非显示指明无返回值，否则都是会生成计算结果的。如：
>val tmp=for (i <- 1 to 3) yield i     //Seq(1,2,3)
def relu(x:Double)=if(x<0) 0.0 else x  

3. **Scala集合**
3.1 Scala实现了两套集合系统（immutable and mutable）immutable 集合在添加删除元素时，生成一个新的集合，原来的集合并未发生变化，而mutable集合是对原有的集合进行操作，并未产生新集合。通过一些函数组合子（Functional Combinators）对集合进行操作。常见的集合类型包括：
  - 3.1.1 List构造列表的两个基本单位是 Nil 和 ::，Nil表示为一个空列表。对于List有三个基本操作：（1）head返回列表的第一个元素，（2）tail返回除了第一个元素外的其他元素；（3）isEmpty判断列表是否为空。
  - 3.1.2 Set元素不重复。
  - 3.1.3 Tuple元组中可以包含不同类型的元素。
  - 3.1.4 Map 包含三个基本操作：keys、values、isEmpty
  - 3.1.5 Option是一个表示有可能包含值得容器，实现了一个基本的接口。Option本身是泛型的，并且有两个子类： Some[T] 或 None。
>trait Option[T] {
  def isDefined: Boolean
  def get: T
  def getOrElse(t: T): T
}

 3.2 一些常见的函数组合子(Functional Combinators)包括：
 map/foreach/zip/filter/partition/find/drop/fold/flatMap。用法略

 3.3 Scala集合和Java集合之间的相互转化。用asScala 装饰常用的Java集合以和用asJava 方法装饰Scala集合.
  - 相互转化
  >scala.collection.Iterable = java.lang.Iterable
scala.collection.Iterable = java.util.Collection
scala.collection.Iterator = java.util.{ Iterator, Enumeration }
scala.collection.mutable.Buffer = java.util.List
scala.collection.mutable.Set = java.util.Set
scala.collection.mutable.Map = java.util.{ Map, Dictionary }
scala.collection.mutable.ConcurrentMap = java.util.concurrent.ConcurrentMap

  - 单项转化
  >scala.collection.Seq => java.util.List
scala.collection.mutable.Seq => java.util.List
scala.collection.Set => java.util.Set
scala.collection.Map => java.util.Map

* **Scala类型系统**

名称               |含义Scala            |标记
------------       | -------------      |   ------------
协变covariant      |C[T’]是 C[T] 的子类  |[+T]
逆变contravariant  |C[T] 是 C[T’]的子类  |[-T]
不变invariant	   |C[T] 和 C[T’]无关    |[T]
Scala的类型系统必须同时解释类层次和多态性。类层次结构可以表达子类关系。在混合OO和多态性时，一个核心问题是：如果T’是T一个子类，Container[T’]应该被看做是Container[T]的子类吗？变性（Variance）注解允许你表达类层次结构和多态类型之间的关系。子类型关系的真正含义：对一个给定的类型T，如果T’是其子类型，你能替换它吗？（参照引用）

* **Future和Promise区别**

所谓Future，是一种用于指代某个尚未就绪的值的对象。而这个值，往往是某个计算过程的结果：

  1. 若该计算过程尚未完成，我们就说该Future未就位；
  2. 若该计算过程正常结束，或中途抛出异常，我们就说该Future已就位。

Future的就位分为两种情况：

  1. 当Future带着某个值就位时，我们就说该Future携带计算结果成功就位。
  2. 当Future因对应计算过程抛出异常而就绪，我们就说这个Future因该异常而失败。

Promise 承诺返回Future计算的值，允许你在 Future 里放入一个值，不过只能做一次，Future 一旦完成，就不能更改了。


参考资料：https://twitter.github.io/scala_school/zh_cn/index.html


### Spark调优技巧
- Spark不同的配置类型，包括：（1）Spark的应用环境如配置模式（client和cluster）、master的URL、Driver的信息等；（2）运行时环境，包含的Java类库、Java虚拟机的配置等；（3）**Shuffle的策略**：map文件是否压缩，文件缓存等。（4）Spark UI的配置。（5）**压缩和序列化的配置**，通常的尽量使用官方推荐的Kryo序列化库，广播变量、shuffle过程中的数据都默认使用lz4压缩，而RDD只有序列化后才能压缩，通常使用压缩会增加性能开销。（5）**内存管理配置**：包括Spark的执行内存（execution）和存储内存(storage),是否开启offHeap，已经offHeap的大小等。（6）**动态分配**（Dynamic Allocation），如配置initialExecutors/minExecutors/maxExecutors等，注意需要shuffle.service.enabled。（7）安全控制配置；（8）**SparkSQL配置**，包括配置spark.sql.codegen，从而获取更好的表达式查询速度。（9）Spark Streaming相关配置（略）。
### Spark基本概念

**RDD** 是Spark的基本数据类型之一，类似单机编程中的数组，可以执行map、reduce等操作。RDD分区存储在不同的机器上保持冗余，可以被并行处理。创建RDD有两种方法：（1）普通对象转化，（2）从文件系统或者HDFS读取。

常见的RDD操作分为**transformation和action**: transformation对RDD进行转化，如map、filter等操作，transformation生成的RDD只依赖父RDD称之为narrow dependency，通常是惰性的，action对RDD进行计算，如reduce、collect，join等，如c=a.join(b)有可能产生wide dependency或ShuffleDependency。一些常见的操作包括：

Map、MapPartition(对每个分区中的内容进行处理，每个分区中的内容以Iterator[T]接受)、MapValues（对k-v中的每个values进行函数map操作）、flatMap（对每个RDD元素生产一个RDD数组类似Hive中的explode）、flastMapValues(对于k-v中的每个values进行flatMap)、Reduce、reduceByKey(对k-v中相同k的values进行reduce操作，类似mysql的group函数)。

RDD编译时类型安全，能检查出类型错误便于进行函数式编程。但由于RDD是val不变型对象，势必不断创建新的对象造成GC，其次是RDD序列化和反序列化的性能开销。（可以考虑惰性求值等方法进行编程）

RDD的**容错恢复机制**：**lineage和checkpoint**。lineage追踪RDD在DAG计算图中的依赖，并基于检查点进行恢复。具体来说Spark提供cache/persist和checkpoint。当调用cache函数时，Spark将这个数据对象保存在内存中，RDD转化为persistRDD。persist可以提供多种storageLevel的存储。如果是MEMORY\_ONLY，persist和cache方法相同。通过unpersist可以手动移除持久化数据。

checkpoint将RDD保存在HDFS中并遗忘lineage信息，改变了RDD的DAG图信息，在下一次调用Driver程序时可以使用checkpoint中的数据。而persist\(StorageLevel.DISK\_ONLY\)只能保存RDD在硬盘中，当程序结束后blockManager会删除这些persist的数据。

广播变量Broadcast是一个read-only的数据对象，可以将数据发送到每个计算节点上，便于进行join等操作。有两种类型的广播变量HttpBroadcast和TorrentBroadcast。

**DataFrame** 将每一行的数据存在一个schema对象中，此外DataFrame是off-heap的，直接受操作系统管理。但DataFrame不是类型安全的，如果将某个列的int类型和string进行比较，编译时期不会报错。

**DataSet** 结合了RDD和DataFrame的优点。即可以获取每个columns的数据类型，也是编译时类型安全的。

### SparkSQL和HiveOnSpark
HiveOnSpark 是将Hive的计算引擎由MapReduce改为Spark，提供DAG执行计划，加快了Hive的查询速度，类似的项目有HiveOnTez。

SparkSQL 可以读取Hive表、RDD、JSON外部数据表等，使用SparkSQL进行计算。SparkSQL提供的SQL查询函数不如Hive丰富。

### Spark和Hadoop的Shuffle比较
hadoop的Shuffle机制是基于排序方法的。
Spark的Shuffle机制有sort-based和hashmap两种。

### Spark内存管理
Spark内存布局分为Execution内存和Storage内存。1.5以前使用StaticMemoryManager，但这种方式不能适应不同记得计算场景。1.6以后采用UnifiedMemoryManager。
**Storage内存**，用来缓存Task数据、在Spark集群中传输（Propagation）内部数据；
**Execution内存**，用于满足Shuffle、Join、Sort、Aggregation计算过程中对内存的需求。
使用UnifiedMemoryManager可以动态伸缩。在storage和execution中抽象出soft boundary。当某一个内存区中内存用量不足的时候，可以从另一个内存区中借用。


参考资料：

关于Spark内部原理：https://github.com/JerryLead/SparkInternals

关于Spark Shuffle：http://jerryshao.me/architecture/2014/01/04/spark-shuffle-detail-investigation/
