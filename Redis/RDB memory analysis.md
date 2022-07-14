# RDB memory analysis



## 1. 为什么要对Redis进行内存分析

Redis运行久了，内部经常会堆积些冗余数据，或者不合理的使用也会导致内存的占用

内存比磁盘贵，优化了内存占用就是省钱



## 2. 怎么构建内存分析数据

### 2.1 下载近期的冷备RDB文件

下载RDB文件，将他放置到性能比较好的机器上

### 2.2 安装rdbtools

```
pip install rdbtools
```



### 2.3 RDB导出为csv文件

> 看自己需求是分析全量数据，还是分析占比较多的数据，按需选择

导出全量数据：

```
rdb -c memory /userdata/tmp_20211019.rdb > redis_memory_report.csv
```

导出内存占用大于128 bytes的数据：

```
rdb -c memory /userdata/tmp_20211019.rdb --bytes 128 -f redis_memory_report.csv
```



### 2.4 Mysql中新建临时表

```
CREATE TABLE `temp_memory_20211019` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `database` int(128) DEFAULT NULL COMMENT 'key在redis的db',	
  `type` varchar(128) DEFAULT NULL COMMENT 'key类型',
  `KEY` varchar(128) DEFAULT NULL COMMENT 'key值',
  `size_in_bytes` bigint(20) DEFAULT NULL COMMENT 'key的内存大小(byte)',
  `encoding` varchar(128) DEFAULT NULL COMMENT 'value的存储编码形式',
  `num_elements` bigint(20) DEFAULT NULL COMMENT 'key中的value的个数',
  `len_largest_element` varchar(128) DEFAULT NULL COMMENT 'key中的value的长度',
  `expiry` datetime(6) DEFAULT NULL COMMENT 'key过期时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='RDB数据分析临时表';
```



### 2.5 Mysql命令行中导入数据

```
LOAD DATA INFILE '/tmp/redis_memory_report.csv' 
INTO TABLE temp_memory_20211019
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(`database`,`type`,`KEY`,`size_in_bytes`,`encoding`,`num_elements`,`len_largest_element`,`expiry`);
```



### 2.6 表加索引

> 常用字段加上索引，便于分析

```
alter table temp_memory_20211019 add index idx_key(`key`),add index idx_expiry(expiry),add index idx_size_in_bytes(size_in_bytes);
```

至此，准备工作就做好了



## 3. 具体分析什么

> 以下列举一些常用的分析需求

### 3.1 查询key的个数

```
select count(*) from temp_memory_20211019;
```



### 3.2 查询总的内存占用

```
select sum(size_in_bytes) from temp_memory_20211019;
```



### 3.3 查询内存占用最高的10个key

```
select * from temp_memory_20211019 order by size_in_bytes desc limit 10;
```



### 3.4 查询value个数1000个以上的list

```
select * from temp_memory_20211019 where type=’list’ and num_elements >= 1000;
```



### 3.5 查询哪些业务占用内存较高

```
SELECT `key`,COUNT(1),SUM(size_in_bytes) sumData FROM temp_memory_20211019 GROUP BY substr(`key`,1,5) ORDER BY sumData DESC;
```



### 3.6 查询某业务总占用内存

```
SELECT SUM(size_in_bytes) sumData FROM temp_memory_20211019 where `KEY` LIKE 'sc:%'
```



### 3.7 查询某业务内key分别占用内存

```
SELECT `KEY`,size_in_bytes sumData FROM temp_memory_20211019 where `KEY` LIKE 'sc:%'
```










