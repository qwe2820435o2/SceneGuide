# Link Of The Persistence

## 1. Persistence Process
> The point is to reduce lock conflicts

![Counting Design — Persistence details](../Material/image/Counting%20Design%20—%20Persistence%20details.png)


## 2. Timing Persistence
> Execute once every 2 minutes, and persist the incremental count of Redis to the Mysql database

### 2.1 Time Window

* Each business field corresponds to a time window Set collection