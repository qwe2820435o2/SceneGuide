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

The Collecting data is strongly related to the business, such as: comments, likes, favorites, etc

Only after the operation is completed, we will report the buried point
```

## 2. Technology Selection

```
The daily magnitude of the data uploading interface is 100 million

In view of this, we need to carefully evaluate the characteristics of each component and choose

CDN: dynamic acceleration, intelligent selection of better routes back to source acquisition
Nginx: excellent reverse proxy server
RabbitMQ: the functions are relatively comprehensive, which can meet a variety of usage scenarios
Kafka: high-performance, low-latency messaging middleware
Flink: high-performance, low-latency streaming computing
Redis: distributed cache with excellent performance and rich data types
Caffeine: excellent local cache

```

## 3. Architecture design

![Data collecting design](../Material/image/Data%20collecting%20design.png)

## 4. Link design

### 4.1 Behavior collecting

```markdown
Behavior burying interface requests a lot

In addition to simply verifying the accuracy of the data here, the information should be directly sent to the big data Kafka
```

### 4.2 Business collecting

```markdown
Due to the characteristics of the business buried point, the secondary forwarding after processing is required here

The information is first sent to RabbitMQ, processed by its consumers, and then the data is sent to the big data Kafka
```

## 5. Implementation details

### 5.1 Behavior collecting

#### 5.1.1 Upload time

```markdown
Due to network differences, the client will be divided into offline reporting and real-time reporting

In the case of a weak network, report offline, that is: store locally, and report in batches when the network is smooth

When the network is good, report directly in batches
```

#### 5.1.2 Prevent duplicate upload

```markdown
The daily data volume of behavioral buried points is too large to perform real-time deweighting, which will affect performance

Therefore, data is stored first, and T+1 deweighting is performed on the big data side
```

#### 5.1.3 Data format

**Format:**

```markdown
Request：POST     application/x-www-from-urlencoded

{
    "commonParams":{
        "extend_data":"",
        "os":"android",
        "lan":"en",
        "imei":"89fc9bcffcb84959",
        "imsi":"4ac123bcb615a5dc"
    },
    "events":"7615ffdbbb1f4e5f9b55ad010852848b"
}
```












