# Link Of The Consumption

## 1. Parsing DTO

Parse SendReq

Map table and field according to field tableType and fieldType respectively

## 2. Weaken the shaving of Consumption

In order not to process too much data at one time, the delay queue is used for weaken the shaving

* The popularity of Col, Music, and Video is regularly calculated for recommendation and search rankings every day
* 1000 batches, calculate the delayTime, and the time interval between each batch is 6 seconds, so that a large batch of data updates can be evenly distributed to each time window
* The message will be stored in the delay queue. Whenever the delayTime is reached, it will be sent to the count queue for consumption

![Counting Design (3) - Weaken the shaving of Consumption](../../Material/image/Counting%20Design%20(3)%20-%20Weaken%20the%20shaving%20of%20Consumption.png)

## 3. Full Counting Cache
> Warm up the full counting cache for user interface display, for example: the total number of playlists is 100,000, and every time you listen to a song, it will be +1 on its basis

### 3.1 Data Structure
> Select the data structure as Hash

```Select the data structure as Hash
The key of Col:
count:all:c:{colId}

field:
collect、comment、share、stream、download、popular

value:
total value
```

```Select the data structure as Hash
The key of Music:
count:all:m:{musciId}

field:
download、collect、share、stream、popular

value:
total value
```

### 3.2 Build Process

#### 3.2.1 Data Construction

1. Assemble Redis key according to Id and Field

2. hasKey() Determines whether the key exists

3. hincrBy +1 to the number of fields

4. When the key does not exist and fieldCount=1, check the database to preheat the cached data

   ```
   if (!exist && 1 == fieldCount){
   	//query Mysql
   }
   ```

5. Renew to ensure that the hotspot data does not expire


#### 3.2.2 Data Consistency
> In principle, redis data is unreliable due to problems such as cache failure, memory recycling, and persistence strategy selection, and the data in mysql shall prevail

* The cache invalidation time is 8 hours to ensure the final consistency of the cache and database data
* Check the cache first, if not, check it from the database
* Data changes during the period, through HINCRBY cache key & field synchronization changes
* The timed task monitors the difference between the Redis value and the Mysql value. If the difference is too large, delete the cache and re-warm the data from Mysql


## 4. Delta Cache
> Record incremental operations in real time, such as: a song list is listened to by the user for the first time, and its incremental playback number is 0, it will be +1 on the basis of it

### 4.1 Data Structure
> Select the data structure as Hash


```
The key of Col:
count:dyn:c:{colId}

Field:
collect、comment、share、stream、download、popular

value:
changing value
```

```
The key of Music:
count:dyn:m:{musciId}

Field:
download、collect、share、stream、popular

value:
changing value
```

### 4.2 Data Construction

1. Assemble Redis key according to Id and Field
2. hincrBy +1 to the number of fields
3. Renew to ensure that the hotspot data does not expire

## 5. Time window
> Time window composed of Redis Set

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








