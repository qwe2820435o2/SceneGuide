# Subsequent optimization

## 1. Warm Cache

* Scheduled tasks perform Redis cache and local cache preheating for popular data in advance
* Try to use asynchronous preheating for preheating, you can use message queues, which can be asynchronous and take into account performance

## 2. Circuit Breaker And Downgrade

* Overload protection for the interface

