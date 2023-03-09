# Send To A Device Group
> Send a message to the device according to the registration token of the device

## 1. Sending Process

![Fcm Pushing Design (2) - Process](../../Material/image/Fcm%20Pushing%20Design%20(2)%20-%20Process.png)

## 2. Optimize Direction

### 2.1 Data Query

#### 2.1.1 Storage and Efficiency

**Past：**

```
In the past we used Impala

But Impala's query performance is terrible

We've been actively looking for alternatives until we met Clickhourse
```

**Current：**

```
After research and comparison, we chose ClickHouse

ClickHouse is columnar storage, we can query Device's Token faster
```


#### 2.1.2 Multithreading

```
Open the thread pool and assign a thread to each task for Clickhouse query

Send the found data to the message queue in batches
```



#### 2.1.3 Load Balancing



#### 2.1.4 Splitting Large Table



### 2.2 Data Sending

#### 2.2.1 Adjust Single Batch Quantity



#### 2.2.2 Multithreading