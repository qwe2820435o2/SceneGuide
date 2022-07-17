# Client error that could not get a resource from the pool

## 1. 原因&解决方案

* 并发确实太高，链接池配置参数不合理

  解决方案：调整配置参数；扩容节点

* Redis执行队列被大量操作或者耗时操作占用

  解决方案：优化慢操作；禁止慢操作

* 存在热key

  解决方案：拆分key，分散压力到各个redis节点；增加本地内存，先查本地内存，查不到再去redis

* 某个节点链接池耗尽

  解决方案：解决数据倾斜问题

* 执行耗时命令导致ping超时

  解决方案：禁用耗时命令，如：keys *；优化耗时操作

* 低版本的Jedis包存在bug

  解决方案：升级Jedis版本
  
  
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