# Data backup and recovery

## 1. persistent configuration strategy

### 1.1 RDB

RDB is the default persistence method of Redis, which will generate data files according to the configured strategy

The default generation strategy of RDB: save 60 10000, which can be flexibly adjusted according to the data volume of our own application and business



### 1.2 AOF

Redis logs all commands that have written to the database to an AOF file

AOF is not enabled by default 

It is enabled or not depends on the sensitivity of the business

Redis currently supports three AOF save modes:

  1. AOF_FSYNC_NO ：do not save
  2. AOF_FSYNC_EVERYSEC ：save every second
  3. AOF_FSYNC_ALWAYS ：Save every time that a command is executed



 ## 2. data backup solution

RDB is very suitable for cold backup. After each generation, it will not be modified again.

Data backup plan:

  1. Write crontab schedule script to do data backup
  2. Copy a backup of rdb every hour to a directory and keep only the backups of the last 48 hours
  3. Keep a backup of the rdb every day go to a directory and keep only the backup of the last month
  4. Every time you copy a backup, you should delete the old backup.
  5. Backup all data on the current server every night and send a copy to S3



## 3. 场景模拟

### 3.1 Redis进程挂掉

**解决方案**：重启redis进程即可，直接基于AOF日志文件恢复数据



### 3.2 Redis进程所在机器挂掉

**解决方案**：重启机器后，尝试重启redis进程，基于AOF日志文件进行数据恢复；如果AOF文件破损，可通过redis-check-aof fix命令修复



### 3.3 Redis进程挂掉，并且AOF文件丢失

**解决方案**：基于该机器上当前的某个最新的RDB数据副本进行数据恢复



### 3.4 Redis进程挂掉，AOF文件丢失、RDB文件丢失

**解决方案**：在S3上找到RDB最新的一份备份，copy到redis里面去，就可以恢复当时时间点的数据

**注意**：

如果遇到了场景（3）、（4），直接拷贝最新的RDB数据副本过去，哪怕删掉了aof文件，重启后数据是没法恢复的

因为虽然我们删除了aof文件，但是因为打开了aof持久化，redis就一定会优先基于aof去恢复，即使文件不在，那就创建一个新的空的aof文件

因为虽然我们删除了aof文件，但是因为打开了aof持久化，redis就一定会优先基于aof去恢复

即使文件不在，那就创建一个新的空的aof文件

在数据安全丢失的情况下，基于rdb冷备，如何完美的恢复数据，同时还保持aof和rdb的双开呢？

正确操作步骤：

  1. 停止redis
  2. 配置中关闭aof
  3. 拷贝rdb备份
  4. 重启redis
  5. 确认数据是否恢复
  6. 直接在命令行热修改redis配置,打开aof

这个时候redis就会将内存中的数据对应的日志，写入aof文件中

