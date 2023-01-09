# Link Of The Consumption

###  Time window
> Time window for step 5

Mainly to reduce granularity and dynamically obtain changing values

The purpose is to optimize the stacking statistics performance

**Solution:** 

Borrow the concept of a time window, take each time of the scheduled task as the benchmark, divide 1 day into multiple time windows, and only operate the aggregated data corresponding to the time window

| Timing scheduling cycle | Number of splittable time windows in 1 day | Rules corresponding to Set keys |
| :---------------------: | :----------------------------------------: | :-----------------------------: |
|       10 minutes        |                24 * 6 = 144                |       item:g:20220720:88        |

* Add

Get the current timestamp, calculate the time window index of the current day in the code, and then add data to the corresponding collection

* Delete

Because the Set collection is associated with the date and time window, the expiration time can be set for the Set. It is recommended to be longer than the scheduled scheduling period, 15 minutes is appropriate

* Query

Get the current timestamp, calculate the time window index of the current day in the code, and then query the data in the corresponding collection