# Link Of The Persistence

## 1. Persistence Process
> The point is to reduce lock conflicts

![Counting Design — Persistence details](../../Material/image/Counting%20Design%20—%20Persistence%20details.png)


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

### 2.2 Batch query incremental statistics
> In order to further optimize performance, introduce Pipeline to check Redis cache


* Pipeline check Set Field time window
* Pipeline sets the time window expiration time
* Pipeline check Hash incremental statistics

### 2.3 Batch Processing

Although the day has been split into multiple time windows, it is still possible that the processing volume will be high during peak periods


Excessive one-time processing will greatly consume database performance

A batch of 50,000 is tentatively set. When it is greater than this number, it will be split into multiple batches and processed in batches


### 2.4 Batch Update To Database

Bulk update using INSERT ... ON DUPLICATE KEY UPDATE Statement


```
insert into music (musicId,
    collect,
    comment,
    share,
    stream,
    download,
    popular
    )
    values
    <foreach collection="list" item="musicItem" index="index" separator=",">
      (#{musicItem.musicId},
      #{musicItem.collect},
      #{musicItem.comment},
      #{musicItem.share},
      #{musicItem.stream},
      #{musicItem.download},
      #{musicItem.popular}
      )
    </foreach>
    on duplicate key update
    collect = collect + values(collect),
    comment = comment + values(comment),
    share = share + values(share),
    stream = stream + values(stream),
    download = download + values(download),
    popular = popular + values(popular)
```








