# Link Of The Query


## 1. Interface Type

### 1.1 Single Item Statistics Query
> This interface is suitable for business scenarios that are highly sensitive to statistical changes, such as: song list details page

Query the corresponding collect, comment, share, stream, download and other values according to the Primary Id

### 1.2 Single Ttem Statistics Query (increase local cache)
> This interface is suitable for business scenarios with moderate sensitivity to statistical changes and high concurrency, such as: Embed sharing page

Compared with 1.1, introduced caffeine local cache for performance optimization

### 1.3 Batch Item Statistics Query

This interface is suitable for batch query business scenarios, such as: album rankings, homepage playlist list

## 2. Interface Details

### 2.1 Redis Cache

In order to avoid a large number of queries directly penetrating to the Mysql database, we use Redis as a cache to enhance the anti-concurrency capability

