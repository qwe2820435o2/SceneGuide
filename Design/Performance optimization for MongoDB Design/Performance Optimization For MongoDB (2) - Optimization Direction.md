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

## 6. Slow Queries

