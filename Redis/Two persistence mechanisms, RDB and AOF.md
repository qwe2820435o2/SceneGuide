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


```