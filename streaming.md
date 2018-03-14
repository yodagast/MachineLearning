###流式计算

#### 流式计算主要问题

(1) **Exactly-once guarantees**: state in stateful operators should be correctly restored after a failure
(2) **Low latency**: the lower the better. Many applications require sub-second latencyhigh-thorughput(Spark DStream/1S-10S, Structured Streaming/1ms, Flink/1ms)   
(3)**High throughput**: pushing large amounts of data through the pipeline is crucial as the data rates grow
(4)**Flow control**: **backpressure **from slow operators should be naturally absorbed by the system and the data sources to avoid crashes or degrading performance due to slow consumers.
(5)fast recovery after a failure
(6)**Powerful computation model**: the framework should offer a programming model that does not restrict the user and allows a wide variety of applications
(7) Low overhead of the fault tolerance mechanism in the absence of failures

#### 不同系统对比

- **Apache Storm** ( upstream backup and record acknowledgements, At-least-once,**low latency**,low thorughput)
- **Spark Streaming**(Micro batches,**exactly-once**,low latency,**high throughput**)
- **Google Cloud Dataflow** (Transactional updates)
- **Apache Flink/Strucured Streaming** (Distributed Snapshots,**low latency**, **high throughput**, exactly-once)：Flink’s variation of the [Chandy Lamport algorithm](https://blog.acolyer.org/2015/04/22/distributed-snapshots-determining-global-states-of-distributed-systems/) periodically draws state snapshots of a running stream topology, and stores these snapshots to durable storage (e.g., to HDFS or an in-memory file system),regular data processing always keeps going, processing events as they come, while checkpoints happen in the background.(和Spark Streaming的不同，Streaming需要定时写checkpoint到hdfs，可能产生瓶颈)

#### backpressure


参照：（1）Flink 分布式快照算法 https://blog.acolyer.org/2015/04/22/distributed-snapshots-determining-global-states-of-distributed-systems/
（2）YAHOO Spark/Storm/Flink对比https://www.slideshare.net/HadoopSummit/performance-comparison-of-streaming-big-data-platforms
（3）反压 https://www.linkedin.com/pulse/enable-back-pressure-make-your-spark-streaming-production-lan-jiang/
（4）Spark Streaming 系统关键点 https://www.gitbook.com/book/jaceklaskowski/spark-structured-streaming/details
（5）Twitter Heron https://blog.twitter.com/engineering/en_us/a/2015/flying-faster-with-twitter-heron.html



