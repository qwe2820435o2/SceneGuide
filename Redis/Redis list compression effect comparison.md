# Redis list compression effect comparison

## 1. Before turning on compression

|     Memory     | Redis Itself takes up | after |
| :------------: | :-------------: | :-------------: |
| used_memory | 848656 | 2879416 |
| used_memory_human | 828.77K | 2.75M |
| used_memory_rss | 2867200 | 4931584 |
| used_memory_rss_human | 2.73M | 4.70M |


## 2. Compression is enabled, compression depth =1


## 3. Turn on compression before the JDK way serialization


## 4. Open compression, JDK way serialization, compression depth =1


## 5. Serialization in Json mode before turning on compression


## 6. After compression is enabled, it is serialized in Json mode with compression depth =1