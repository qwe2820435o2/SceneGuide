# Optimization Direction

## 1. Security
```
Due to historical reasons, authority authentication was not configured before, and there are certain security risks

Therefore, this time we need to improve the authentication mechanism and add permission control
```

## 2. Version
```
We are currently using version 3.X

Plan to upgrade to version 4.4 or 5.0

There are many benefits of upgrading, such as:
1. Support new features and functions
2. The underlying implementation has been optimized to reduce the impact of lock conflicts and enhance query efficiency
```


## 3. Shard Key
```
The selection of individual Collection shard keys is unreasonable, resulting in a sharp increase in CPU utilization when query operations are concurrently high

In view of such a situation, it is necessary to conduct a comprehensive evaluation based on business characteristics and query characteristics, and select a more reasonable sharding key
```

## 4. Secondary Node
```
In the past, the role of the Secondary Node was as a redundant copy, which was not utilized, which was actually a waste of resources.

Now, we plan to separate read and write, make full use of the Secondary Node, add, delete and modify operations on the master node, and query operations on the slave node
```

## 5. Historical Data
```
Some of the data we store in MongoDB is associated with the timeline

For example: Feed Streaming related

From a business point of view, we only need to maintain the data of the last half year, because users will only pay attention to the news of the last half year

We can put the data out of timeliness on AWS S3 for backup
```

## 6. Slow Queries
```
We use a lot of MongoDB services, some unfriendly use will also lead to slow query, slow query will cause the CPU to soar and affect the performance of the interface

For example:
Pagination query: increase the sort_id field, bring the last _id record of the previous page each time you query, replace skip with gt or lt to reduce the number of scanned documents
```
