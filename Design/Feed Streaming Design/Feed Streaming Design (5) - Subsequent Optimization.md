# Subsequent Optimization

## 1. Warm Up The Cache

* Scheduled tasks perform Redis cache and local cache preheating for hot messages in advance
* Try to use asynchronous preheating for preheating, you can use message queues, which can be asynchronous and take into account performance

## 2. Introduce Circuit Breaker Downgrade

* Overload protection for the interface
* Isolate third-party resources with slow response
* Return friendly pocket data after fusing

## 3. Improve Monitoring

* Dubbo thread pool
* Tomcat thread pool
* JVM monitoring
* Caffeine cache usage and hit rate monitoring
* Redis connection pool
* Business monitoring

## 4. Asynchronization
> The RPC interface for sending messages provided externally, the encapsulation level needs to be further improved

```
Asynchronization is to further optimize interface performance

The business of sending messages can be completely asynchronous, and there is no need to perform operations such as plugging and cutting messages in the synchronous call interface

The RPC interface internally sends to MQ for asynchronous processing, and then directly returns success information
```

## 5. Data Structure Optimization
> The message storage structure in Redis is List, but the actual experience is not satisfactory

### 5.1 Business Use

**Old Logic:**

![Feed Streaming Design (5) - Business Use](../../Material/image/Feed%20Streaming%20Design%20(5)%20-%20Business%20Use.png)

**Shortcoming:**
1. Need to check and save
2. It takes extra time to traverse

**New Data Structure:**

```
Reids -> zset

key -> xxx:{userId}
field -> timestamp
value -> msg content

Using this data structure is not only convenient for query and cutting, but also saves traversal time
```