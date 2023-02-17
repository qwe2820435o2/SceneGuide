# Subsequent Optimization

## 1. Warm Up The Cache

* Scheduled tasks perform Redis cache and local cache preheating for hot messages in advance
* Try to use asynchronous preheating for preheating, you can use message queues, which can be asynchronous and take into account performance

## 2. Introduce Circuit Breaker Downgrade

* Overload protection for the interface
* Isolate third-party resources with slow response