# Memory usage optimization



## 1. Utilize jemalloc memory allocation feature for optimization

In a 64-bit system, jemalloc divides the memory space into three ranges: small, large and huge

Each range is divided into many small memory block units

When Redis stores data, it will select the memory block with the most suitable size for storage

As shown in the figure：

![Jemalloc memory](../Material/image/Jemalloc%20memory.png)

The values are discontinuous when jemalloc allocates memory

Therefore, if the key/value string changes by one byte, it may cause a large change in memory usage. 

This can be used in design.


E.g:

If the length of the key is **8 bytes**, the SDS is 8+9=**17 bytes**, and jemalloc allocates **32 bytes**

At this time, the key length is reduced to **7 bytes**, then the SDS is **16 bytes**, and jemalloc allocates **16 bytes**

Then the space occupied by each key can be reduced by half


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

![Compressed size](../Material/image/Compressed size.png)

  







