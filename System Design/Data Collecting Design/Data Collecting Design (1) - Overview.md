# Data collecting design

## 1. Overview

### 1.1 Behavior collecting

```
The client collecting

Collect user behavior data, such as: listening time, icon clicks, redirected pages, etc

Upload in batches and perform data cleaning on the reported data

```

### 1.2 Business collecting

```
The server collecting

The Collecting data is strongly related to the business, such as comments, likes, favorites, etc

Only after the operation is completed, we will report the buried point
```

## 2. Technology Selection

```
The daily magnitude of the data-uploading interface is 100 million

Because of this, we need to carefully evaluate the characteristics of each component and choose

CDN: dynamic acceleration, intelligent selection of better routes back to source acquisition
Nginx: excellent reverse proxy server
RabbitMQ: the functions are relatively comprehensive, and can meet a variety of usage scenarios
Kafka: high-performance, low-latency messaging middleware
Flink: high-performance, low-latency streaming computing
Redis: distributed cache with excellent performance and rich data types
Caffeine: excellent local cache

```

## 3. Architecture design

![Data collecting design](../../Material/image/Data%20collecting%20design.png)



