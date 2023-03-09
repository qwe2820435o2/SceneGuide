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

```
We link to Clickhouse using a local domain name

Query tasks will be evenly load-balanced to multiple Clickhouse nodes to avoid the problem of excessive pressure on a single point

Advantages: load balancing, can cope with changes
Cons: May charge a small fee
```



#### 2.1.4 Splitting Large Table

```
Currently analyzing business, data blocks can be divided according to the two dimensions of version and country

Optimization Method:
1. Combining the two dimensions of version and country into tables
2. The Fcm service assembles the table name according to these two dimensions, and directly query the specified table
3. The original single-table offset becomes each sub-table has its own offset

Advantages: There will be much less data in a single table, and the query efficiency will be higher
Disadvantages: The implementation method is more complicated and needs further verification
```



### 2.2 Data Sending

#### 2.2.1 Adjust Single Batch Quantity

```
It is written in the official Google document that the maximum single sending amount of the API is 500/batch


```


#### 2.2.2 Multithreading