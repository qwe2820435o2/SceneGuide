# Client error that could not get a resource from the pool

## 1. Cause & Solution

* The concurrency is indeed too high and the link pool configuration parameters are unreasonable

  Solution: 
  
  Adjust configuration parameters and expand nodes

* The Redis execution queue is occupied by a large number of operations or time-consuming operations

  Solution: 
  
  Optimize slow operations and disable slow operations

* hot key exists

  Solution: 
  
  Split the key and distribute the pressure to each redis node
  
  Increase the local memory, check the local memory first, and then go to redis if it cannot be found

* A node's link pool is exhausted

  Solution: 
  
  Solve the data skew problem

* Executing the time-consuming command causes the ping to time out

  Solution: 
  
  Disable time-consuming commands, such as: keys *
  
  Optimize time-consuming operations

* There is a bug in the Jedis package of the lower version

  Solution: 
  
  Upgrade Jedis version
  
  
## 2. 热key场景梳理

**问题01：**

某个区域Ip访问频繁

**解决：**

增加应用本地缓存，lru维护一定数量的热IP



**问题02：**

频繁查询某个大Zset集合

**解决：**

按业务维度进行key拆分；按数据号段进行拆分


## 3. 某个节点链接池耗尽场景梳理

> hashtag滥用引发的血案

![在这里插入图片描述](https://img-blog.csdnimg.cn/54745ba934084854a044cc9610b103c4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5LiA5p2h5b6I6ICB55qE6IWK6IKJ,size_20,color_FFFFFF,t_70,g_se,x_16)