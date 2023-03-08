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



#### 2.1.2 Multithreading and Concurrency



#### 2.1.3 Load Balancing



#### 2.1.4 Splitting Large Table



### 2.2 Data Sending

#### 2.2.1 Adjust Single Batch Quantity



#### 2.2.2 Multithreading And Concurrency