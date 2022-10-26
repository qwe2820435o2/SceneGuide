# RDB memory analysis



## 1. Why In-Memory Profiling for Redis

Redis has been running for a long time and redundant data is often accumulated inside

Unreasonable use will also lead to memory usage

Memory is more expensive than disk, optimizing memory usage is saving money



## 2. How to build memory profiling data

### 2.1 Download recent cold standby RDB files

Download the RDB file and place it on a machine with better performance

### 2.2 安装rdbtools

```
pip install rdbtools
```



### 2.3 RDB export to csv file

> Depending on your needs, whether to analyze the full amount of data or analyze the data that accounts for a large proportion, choose as needed

Export full data:

```
rdb -c memory /userdata/tmp_20211019.rdb > redis_memory_report.csv
```

Export data with a memory footprint greater than 128 bytes:

```
rdb -c memory /userdata/tmp_20211019.rdb --bytes 128 -f redis_memory_report.csv
```



### 2.4 Create a new temporary table in Mysql

```
CREATE TABLE `temp_memory_20211019` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `database` int(128) DEFAULT NULL COMMENT 'The key is in the redis db',	
  `type` varchar(128) DEFAULT NULL COMMENT 'key type',
  `KEY` varchar(128) DEFAULT NULL COMMENT 'key value',
  `size_in_bytes` bigint(20) DEFAULT NULL COMMENT 'The memory size of the key (byte)',
  `encoding` varchar(128) DEFAULT NULL COMMENT 'The storage encoding form of value',
  `num_elements` bigint(20) DEFAULT NULL COMMENT 'The number of values in the key',
  `len_largest_element` varchar(128) DEFAULT NULL COMMENT 'The length of the value in the key',
  `expiry` datetime(6) DEFAULT NULL COMMENT 'key expiration time',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='RDB data analysis temporary table';
```



### 2.5 Import data from Mysql command line

```
LOAD DATA INFILE '/tmp/redis_memory_report.csv' 
INTO TABLE temp_memory_20211019
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(`database`,`type`,`KEY`,`size_in_bytes`,`encoding`,`num_elements`,`len_largest_element`,`expiry`);
```



### 2.6 table plus index

> Common fields are indexed for easy analysis

```
alter table temp_memory_20211019 add index idx_key(`key`),add index idx_expiry(expiry),add index idx_size_in_bytes(size_in_bytes);
```

So far, the preparations are done



## 3. what to analyze

> Here are some common analysis requirements

### 3.1 Query the number of keys

```
select count(*) from temp_memory_20211019;
```



### 3.2 Query the total memory usage

```
select sum(size_in_bytes) from temp_memory_20211019;
```



### 3.3 Query the 10 keys with the highest memory usage

```
select * from temp_memory_20211019 order by size_in_bytes desc limit 10;
```



### 3.4 Query a list with more than 1000 values

```
select * from temp_memory_20211019 where type=’list’ and num_elements >= 1000;
```



### 3.5 Querying which services occupy the most memory

```
SELECT `key`,COUNT(1),SUM(size_in_bytes) sumData FROM temp_memory_20211019 GROUP BY substr(`key`,1,5) ORDER BY sumData DESC;

select substring_index(`key`,'_',3),count(*),sum(size_in_bytes)
from temp_memory_20211019 
group by substring_index(`key`,'_',3)
order by sum(size_in_bytes) desc
limit 100;
```



### 3.6 Query the total memory occupied by a business

```
SELECT SUM(size_in_bytes) sumData FROM temp_memory_20211019 where `KEY` LIKE 'sc:%'
```



### 3.7 Query the memory occupied by the keys in a business

```
SELECT `KEY`,size_in_bytes sumData FROM temp_memory_20211019 where `KEY` LIKE 'sc:%'
```










