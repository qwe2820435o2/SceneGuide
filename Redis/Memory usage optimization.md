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


## 2. Optimize memory with Int/Long

If it is an integer/long , Redis will use int type (8 bytes) storage instead of strings, which can save more space

Therefore, in scenarios where long/integer can be used instead of strings, try to use long/integer



## 3. Optimizing memory with shared objects

Using shared objects can reduce the creation of objects (reduce the creation of RedisObjects) and save memory space

The core idea of Flyweight design pattern is simple:

If an object instance is immutable once created, then there is no need to create the same instance repeatedly, just return a shared instance to the caller

This not only saves memory, but also reduces the process of creating objects and improves the running speed



Give an example in java:

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

Integer creates and caches Integer objects between -128 and 127 by default

，When calling valueOf, if the parameter is between -128 ~ 127, the subscript is calculated and returned from the cache, otherwise a new Integer object is created



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

  







