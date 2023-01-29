# Subsequent optimization

## 1. Warm Cache

* Scheduled tasks perform Redis cache and local cache preheating for popular data in advance
* Try to use asynchronous preheating for preheating, you can use message queues, which can be asynchronous and take into account performance

## 2. Circuit Breaker And Downgrade

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

## 4. Architecture Split

### 4.1 The First Stage

Statistical Counting Service Standalone

### 4.2 The Second Stage

Statistical counting service service split, divided into 3 aspects according to functional modules

```
counting-service     //Provide addition, deletion, modification and query interface operations
counting-bg			 //Queue asynchronous processing related
counting-task        //Timed task related
```

### 4.3 The Third Stage

Improve overload protection, monitoring and preheating measures

### 4.4 The Fourth Stage

Statistical and counting service service split twice, independent statistics and counting query service

```
counting-manage      //Provide background operations for adding, deleting, and modifying interfaces for business reasons
counting-service     //Provide addition, deletion, modification and query interface operations
counting-query       //Provide query interface operation
```