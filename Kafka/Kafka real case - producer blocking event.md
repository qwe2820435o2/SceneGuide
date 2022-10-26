# Kafka real case - producer blocking event

## 1. Background

北京时间2021-12-07 16:00，大数据部门在跑批次任务，导致服务器内存急剧减少，然后ZK、Kafka相继自杀

随之而来的，kafka消息发送失败，并且阻塞了正常功能

## 2. Check

zk部署有3个节点，虽然zk的原leader挂了，但从日志观察到，已经新选举出新leader，暂时可排除嫌疑

随后，我们将目光移向kafka，我这里直接说最终结论吧。

原因：主要是测服topic的分区未设置冗余导致的，未设置冗余，不算真正的高可用

具体细节，我这里就不细说了，有个哥们的文章写得很详细，推荐给大家

[Kafka生产真实案例-生产者阻塞事件](https://blog.csdn.net/RIGHTSONG/article/details/114839511)



