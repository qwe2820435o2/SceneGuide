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