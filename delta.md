### Spark Delta
##### 解决问题
- 同时读写，保证数据的一致性在（ACID transaction）
- 可以高吞吐从大表读数据（Scalablemetadatahandling）
- 遇到错误可以回滚（rollback）或删改（update/delete/merge）
- 在线业务不下线的同时可以重新处理历史数据
- 处理迟到数据而无需推迟下阶段的数据处理

#####思路
- 批处理和流处理统一
- 按需随时重新处理历史事件：基于时间戳或者基于版本
- 独立且弹性拓展计算和存储资源
