# Use pipeline to optimize performance and memory usage



## 1. Time-consuming analysis of request and response

A complete request response that the time consumption is mainly divided into 3 parts：

1. Link creation and recycling

2. network IO

3. Command actual time



example:

Need to query the details of 100 userIds



Conventional practice: traverse 100 keys, loop query, assemble data and return

Recommended practice: mget, pipeline batch acquisition

mget, pipeline saves the time of link creation and recycling, network IO



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









