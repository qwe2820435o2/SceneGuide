# Kafka real case - producer blocking event

## 1. Background

1. 2021-12-07 16:00 Beijing time, running batch tasks
2. The server memory decreased sharply, and then ZK and Kafka committed suicide one after another
3. kafka message sending failed and blocking normal function

## 2. Check

zk部署有3个节点，虽然zk的原leader挂了，但从日志观察到，已经新选举出新leader，暂时可排除嫌疑

随后，我们将目光移向kafka，我这里直接说最终结论吧。

原因：主要是测服topic的分区未设置冗余导致的，未设置冗余，不算真正的高可用

具体细节，我这里就不细说了，有个哥们的文章写得很详细，推荐给大家

[Kafka生产真实案例-生产者阻塞事件](https://blog.csdn.net/RIGHTSONG/article/details/114839511)



