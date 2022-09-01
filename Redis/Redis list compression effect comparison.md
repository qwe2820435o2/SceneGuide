# Redis list compression effect comparison

## 1. Before turning on compression

|     Memory     | Redis Itself takes up | after |
| :------------: | :-------------: | :-------------: |
| used_memory | 848656 | 2879416 |
| used_memory_human | 828.77K | 2.75M |
| used_memory_rss | 2867200 | 4931584 |
| used_memory_rss_human | 2.73M | 4.70M |


## 2. Compression is enabled, compression depth =1

|     Memory     | Redis Itself takes up | after |
| :------------: | :-------------: | :-------------: |
| used_memory | 848480 | 919688 |
| used_memory_human | 828.59K | 898.13K |
| used_memory_rss | 2723840 | 3051520 |
| used_memory_rss_human | 2.60M | 2.91M |


## 3. Turn on compression before the JDK way serialization

|     Memory     | Redis Itself takes up | after |
| :------------: | :-------------: | :-------------: |
| used_memory | 848480 | 1162472 |
| used_memory_human | 828.59K | 1.11M |
| used_memory_rss | 2719744 | 3002368 |
| used_memory_rss_human | 2.59M | 2.86M |

## 4. Open compression, JDK way serialization, compression depth =1

|     Memory     | Redis Itself takes up | after |
| :------------: | :-------------: | :-------------: |
| used_memory | 848656 | 897176 |
| used_memory_human | 828.77K | 876.15K |
| used_memory_rss | 3100672 | 3100672 |
| used_memory_rss_human | 2.96M | 2.96M |

## 5. Serialization in Json mode before turning on compression

|     Memory     | Redis Itself takes up | after |
| :------------: | :-------------: | :-------------: |
| used_memory | 848480 | 1008264 |
| used_memory_human | 828.59K | 984.63K |
| used_memory_rss | 2723840 | 2990080 |
| used_memory_rss_human | 2.60M | 2.85M |

## 6. After compression is enabled, it is serialized in Json mode with compression depth =1

|     Memory     | Redis Itself takes up | after |
| :------------: | :-------------: | :-------------: |
| used_memory | 848656 | 889400 |
| used_memory_human | 828.77K | 868.55K |
| used_memory_rss | 3063808 | 3063808 |
| used_memory_rss_human | 2.92M | 2.92M |
