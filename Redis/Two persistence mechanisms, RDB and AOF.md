# 1. Two persistence mechanisms, RDB and AOF
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

# 2. Advantages of RDB Persistence Mechanism

## 2.1 Section one

```
RDB will generate multiple data files, each of which represents the data of redis at a certain moment

This method of multiple data files is very suitable for cold backup.

This complete data file can be sent to some remote secure storage, such as Amazon's S3 cloud service.

```

## 2.2 Section two

```
RDB has very little impact on the read and write services provided by redis

Redis can maintain high performance, because the main redis process only needs to fork a child process, and let the child process perform disk IO operations for RDB persistence.
```

## 2.3 Section three

```
Compared with the AOF persistence mechanism, it is faster to restart and restore the redis process directly based on the RDB data file

```

# 3. Disadvantages of RDB Persistence Mechanism

## 3.1 RDB data is less than AOF

```markdown
If you want to lose as little data as possible when redis fails, then RDB is not as good as AOF

Generally speaking, RDB data snapshot files are generated every 5 minutes or longer

At this time, you have to accept that once the redis process goes down, the data of the last 5 minutes will be lost.
```

## 3.2 Generation of RDB may affect service

```markdown
Every time RDB executes the RDB snapshot data file generation by forking a subprocess, if the data file is particularly large, it may cause the service provided to the client to be suspended for several milliseconds, or even several seconds
```

# 4. Advantages of AOF Persistence Mechanism

## 4.1 Lose less data

```markdown
AOF can better protect data from loss

Generally, AOF will perform an fsync operation through a background thread every 1 second, and lose up to 1 second of data

```

## 4.2 High write performance

```markdown
AOF log files are written in append-only mode, so there is no disk addressing overhead

The writing performance is very high, and the file is not easy to be damaged

```

## 4.3 AOF log file is written asynchronously

```markdown
Even if the AOF log file is too large, a background rewrite operation occurs, it will not affect the client's read and write

Because when the log is rewritten, the instructions in it will be compressed, and a minimum log that needs to be restored will be created.

When creating a new log file, the old log file is still written as usual

When the new merged log file is ready, swap the old and new log files

```

## 4.4 Suitable as an emergency recovery

```markdown
Commands in the AOF log file are recorded in a very readable way, which is ideal for emergency recovery from catastrophic accidental deletions

For example, accidentally clearing all data with the flushall command

As long as the background rewrite has not occurred at this time, you can immediately copy the AOF file and delete the last flushall command.

Put the AOF file back, and all data can be automatically recovered through the recovery mechanism

```

# 5. Disadvantages of AOF Persistence Mechanism

## 5.1 Bigger than RDB

```markdown
For the same data, AOF log files are usually larger than RDB data snapshot files

```

## 5.2 Lower performance than RDB

```markdown
After AOF is enabled, the supported write QPS will be lower than the write QPS supported by RDB

Because AOF is generally configured to fsync log files every second

Of course, fsync once per second, the performance is still very high

```

## 5.3 AOF file is easily damaged

```markdown

In the past, there was a bug in AOF

when data recovery was performed through the log recorded by AOF, the exact same data was not recovered.

In order to avoid bugs caused by the rewrite process, each rewrite is not based on the old instruction log for merge, but based on the data in the memory at that time to rebuild the instruction


```

# 6. How to choose between RDB and AOF

## 6.1 Don't just use RDB

```markdown
Don't just use RDB as that will cause you to lose a lot of data
```

## 6.2 Don't just use AOF

```markdown
Also don't just use AOF, because there are two problems with that

1. Using AOF for cold backup, without RDB for cold backup, the recovery speed is faster
2. RDB generates data snapshots simply and rudely every time, which is more robust and can avoid bugs in the complex backup and recovery mechanism of AOF
```

## 6.3 How to choose between RDB and AOF

```

1. Don't just use RDB as that will cause you to lose a lot of data
2. Also don't just use AOF, because then there are two problems for two reasons.

First, you use AOF as a cold backup, without RDB as a cold backup, the recovery speed is faster;

Second, RDB generates data snapshots simply and rudely every time, which is more robust and can avoid bugs in the complex backup and recovery mechanism of AOF.

3. Combined use of AOF and RDB persistence mechanisms

Use AOF to ensure that data is not lost, as the first choice for data recovery;

Use RDB for different degrees of cold backup. When AOF files are lost or damaged, you can also use RDB for fast data recovery

```