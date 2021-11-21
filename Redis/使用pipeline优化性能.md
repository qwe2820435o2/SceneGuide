# 使用pipeline优化性能存占用优化



## 1. 请求响应耗时分析

一个完整的请求响应，时间耗费主要分为3部分：

1. 链接的创建与回收

2. 网络IO

3. 命令实际



例：

需要查询100个userId的详情信息



常规做法：遍历100个key，循环查询，组装数据返回

推荐做法：mget、pipeline批量获取

mget、pipeline节省了链接的创建与回收、网络IO的时间



## 2. Redis cluster pipeline实现思路

mget、pipeline不适用于cluster集群模式

要想适用批处理，需要做改造，思路如下：

* 客户端

  计算key落到的slot槽位，然后根据slot槽位与节点的关联关系可以得到key属于哪个节点，然后每个节点开启pipeline执行命令

* 服务端

  key发送到某个节点，若该key属于这个节点，则会返回值；若不属于，则返回重定向信息

* key本身

  通过HashTag可以自己设定将同一类型的key映射到同一个实例上去

  

## 3. pipeline使用前后性能比对

![在这里插入图片描述](https://img-blog.csdnimg.cn/2c35b810789b42f0a441a9e238993962.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5LiA5p2h5b6I6ICB55qE6IWK6IKJ,size_20,color_FFFFFF,t_70,g_se,x_16)









