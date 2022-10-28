# Two persistence mechanisms, RDB and AOF
> RDB persistence mechanism, which performs periodic persistence of data in redis

1. Use as pure memory

```
If we want redis to be used only as a pure memory cache, then all persistence mechanisms of RDB and AOF can be disabled
```

2. How to back up

```
Through RDB or AOF, the data in the redis memory can be persisted to the disk, and then the data can be backed up to other places, such as cloud services
```

3. How to take advantage of backup

```
If redis hangs, the memory on the server and the data on the disk are lost

You can copy the previous data from the cloud service and put it in the specified directory

Restart redis, redis will automatically restore the data in memory according to the data in the persistent data file, and continue to provide external services

```

4. Which recovery data is more complete

```
Both RDB and AOF persistence mechanisms are used at the same time.

When redis restarts, AOF will be used to rebuild the data, because the data in AOF is more complete
```

# Advantages of RDB Persistence Mechanism

1. RDB will generate multiple data files, each of which represents the data of redis at a certain moment

```
This method of multiple data files is very suitable for cold backup.

This complete data file can be sent to some remote secure storage, such as Amazon's S3 cloud service.

```

2. RDB has very little impact on the read and write services provided by redis.