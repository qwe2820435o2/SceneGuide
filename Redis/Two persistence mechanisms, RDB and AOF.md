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