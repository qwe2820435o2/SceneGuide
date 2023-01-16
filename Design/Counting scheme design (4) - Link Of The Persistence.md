# Link Of The Persistence

## 1. Persistence Process
> The point is to reduce lock conflicts

![Counting Design — Persistence details](../Material/image/Counting%20Design%20—%20Persistence%20details.png)


## 2. Timing Persistence
> Execute once every 2 minutes, and persist the incremental count of Redis to the Mysql database

### 2.1 Time Window

* Each business field corresponds to a time window Set collection
* Calculate the current time window key according to the current timestamp
* The active itemId in the time period is stored in the time window

```
例: Col' key:   count:active:c:field:{timeIndex}

count:active:c:collect:20230108:36
count:active:c:comment:20230108:36
count:active:c:share:20230108:36
count:active:c:stream:20230108:36
count:active:c:download:20230108:36
count:active:c:popular:20230108:36
```