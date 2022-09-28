# Counting scheme design

## 1. Background

Business has statistical counting requirements of different dimensions

Now we need to design a general statistical counting scheme


 ## 2. Whole process

The following is the overall flow chart：

`![Counting Design — Whole Process](../Material/image/Counting%20Design%20—%20Whole%20Process.png)
`
## 3. Details

### 3.1 Time window
> Time window for step 5

Mainly to reduce granularity and dynamically obtain changing values

The purpose is to optimize the stacking statistics performance

**Solution:** 

Borrow the concept of time window, take each time of the scheduled task as the benchmark, divide 1 day into multiple time windows, and only operate the aggregated data corresponding to the time window

| Timing scheduling cycle | Number of splittable time windows in 1 day | Rules corresponding to Set keys |
| :---------------------: | :----------------------------------------: | :-----------------------------: |
|       10 minutes        |                24 * 6 = 144                |       item:g:20220720:88        |

* Add

Get the current timestamp, calculate the time window index of the current day in the code, and then add data to the corresponding collection

* Delete

Because the Set collection is associated with the date and time window, the expiration time can be set for the Set. It is recommended to be longer than the scheduled scheduling period, 15 minutes is appropriate

* Query

Get the current timestamp, calculate the time window index of the current day in the code, and then query the data in the corresponding collection

### 3.2 Persistence
> The point is to reduce lock conflicts

![Counting Design — Persistence details](../Material/image/Counting%20Design%20—%20Persistence%20details.png)


### 3.3 Query

In order to further optimize the performance, we use the pipeline for Redis query