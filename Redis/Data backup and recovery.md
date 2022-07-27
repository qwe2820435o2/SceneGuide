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



## 3. scene simulation

### 3.1 Redis process hangs

**solution**：

Just restart the redis process and restore data directly based on the AOF log file



### 3.2 The machine where the Redis process is located hangs

**solution**：

After restarting the machine, you can try restarting the redis process and perform data recovery based on the AOF log file

If the AOF file is damaged, you can use the redis-check-aof command to fix it



### 3.3 The Redis process hangs and the AOF file is lost

**solution**：

Data recovery based on a current copy of the latest RDB data on the machine



### 3.4 Redis process hangs, AOF file is lost, RDB file is lost

**solution**：

Find the latest backup of RDB on S3 and copy it to redis

You can restore the data at that time point

**Notice**：

If you encounter scenarios 3 and 4, copy the latest RDB data copy directly, even if the aof file is deleted, the data cannot be recovered after restarting

Because although we delete the aof file, because the aof persistence is turned on, redis will give priority to recovery based on aof, even if the file is not there, then create a new empty aof file

Because although we deleted the aof file, because the aof persistence is turned on, redis will give priority to recovery based on aof

Even if the file is not there, create a new empty aof file

In the case of data security loss, based on rdb cold backup, how to restore data perfectly, while maintaining the dual open of aof and rdb?

Correct operation steps：

  1. stop redis
  2. Turn off aof in configuration
  3. copy rdb backup
  4. restart redis
  5. Confirm data recovery
  6. Hot modify the redis configuration directly on the command line and open aof

At that time, redis will write the log corresponding to the data in memory into the aof file

