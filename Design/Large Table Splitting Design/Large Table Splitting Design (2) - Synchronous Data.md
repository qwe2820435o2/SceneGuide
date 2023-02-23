# Synchronous Data

## 1. Overview

```
Complete data consists of stock and incremental data
```

![Large Table Splitting Design (2) - Overview](../../Material/image/Large%20Table%20Splitting%20Design%20(2)%20-%20Overview.png)

## 2. Synchronize Stock Data

* Xtrabackup is used to generate data snapshots to new tables
* The current data offset is recorded in preparation for incremental synchronization

## 3. Synchronize Incremental Data

* Cancel is used to monitor binlog logs and it send message to Kafka
* Consuming Kafka messages is equivalent to completing the synchronization of incremental data
