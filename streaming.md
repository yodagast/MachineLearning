###流式计算

- 流式计算主要问题

(1) **Exactly-once guarantees**: state in stateful operators should be correctly restored after a failure
(2) **Low latency**: the lower the better. Many applications require sub-second latencyhigh-thorughput(Spark DStream/1S-10S, Structured Streaming/1ms, Flink/1ms)   
(3)**High throughput**: pushing large amounts of data through the pipeline is crucial as the data rates grow
(4)**Flow control**: **backpressure **from slow operators should be naturally absorbed by the system and the data sources to avoid crashes or degrading performance due to slow consumers.
(5)fast recovery after a failure
(6)**Powerful computation model**: the framework should offer a programming model that does not restrict the user and allows a wide variety of applications
(7) Low overhead of the fault tolerance mechanism in the absence of failures

- **Apache Storm** ( upstream backup and record acknowledgements, At-least-once,**low latency**,low thor****ughput)
- **Spark Streaming**(Micro batches,**exactly-once**,low latency,**high throughput**)
- **Google Cloud Dataflow** (Transactional updates)
- **Apache Flink** (Distributed Snapshots,**low latency**, **high throughput**, exactly-once)
