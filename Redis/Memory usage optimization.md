# Memory usage optimization



## 1. 利用jemalloc内存分配特性进行优化

jemalloc在64位系统中，将内存空间划分为小、大、巨大三个范围；每个范围内又划分了许多小的内存块单位；当Redis存储数据时，会选择大小最合适的内存块进行存储。如图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/096e60079f2843a69274e512d2d5c31b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5LiA5p2h5b6I6ICB55qE6IWK6IKJ,size_10,color_FFFFFF,t_70,g_se,x_16)



由于jemalloc分配内存时数值是不连续的，因此key/value字符串变化一个字节，可能会引起占用内存很大的变动，在设计时可以利用这一点。



例如，key的长度如果是**8个字节**，则SDS为8+9=**17字节**，jemalloc分配**32字节**；此时将key长度缩减为**7个字节**，则SDS为**16字节**，jemalloc分配**16字节**；则每个key所占用的空间都可以缩小一半。



## 2. 使用整型/长整型优化内存

如果是整型/长整型，Redis会使用int类型（8字节）存储来代替字符串，可以节省更多空间。

因此在可以使用长整型/整型代替字符串的场景下，尽量使用长整型/整型。



## 3. 使用共享对象优化内存

利用共享对象，可以减少对象的创建（同时减少了RedisObject的创建），节省内存空间。



享元设计模式的核心思想很简单：如果一个对象实例一经创建就不可变，那么反复创建相同的实例就没有必要，直接向调用方返回一个共享的实例就行，这样即节省内存，又可以减少创建对象的过程，提高运行速度。



举个java中的例子：

```
public static void main(String[] args) {
	Integer i1 = 12 ;
	Integer i2 = 12 ;
	System.out.println(i1 == i2);

	Integer b1 = 128 ;
	Integer b2 = 128 ;
	System.out.println(b1 == b2);
}

true
false
```



Integer 默认先创建并缓存 -128 ~ 127 之间数的 Integer 对象，当调用 valueOf 时如果参数在 -128 ~ 127 之间则计算下标并从缓存中返回，否则创建一个新的 Integer 对象



## 4. 选用适当的数据结构

|     类型     |  编码方式 | 数据结构     |
| :------------: | :-------------: | :-------------: |
| string | raw、embstr、int | 动态字符串编码、优化内存分配的字符串编码、整数编码 |
| hash | hashtable、ziplist | 散列表编码、压缩列表编码 |
| list | linkedlist、ziplist、quicklist | 双向链表编码、压缩列表编码、3.2版本新的列表编码 |
| set | hashtable、ziplist | 散列表编码、压缩列表编码 |
| zset | skiplist、ziplist | 跳跃表编码、压缩列表编码 |



## 5. 缩减key、value的长度

* 缩减key、value的长度

  在设计键时，在完整描述业务情况下，键值越短越好。例：item:i:10086 => 业务:类型:Id

* value长度

  可在序列化方式上进行操作。下图是JAVA常见序列化工具空间压缩对比，如图：

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/274098f1029849e9bf85362c0bdfab89.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5LiA5p2h5b6I6ICB55qE6IWK6IKJ,size_16,color_FFFFFF,t_70,g_se,x_16)

  







