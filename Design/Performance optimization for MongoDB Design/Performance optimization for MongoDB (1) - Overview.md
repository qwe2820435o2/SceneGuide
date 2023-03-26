# Overview

## 1. Background

```markdown
Frequent CPU alarms were reported by the MongoDB server, indicating that its performance needed to be optimized
```


## 2. Existing Problems
> These performance-affecting issues are waiting for us to solve

1. No account and password are set up, you can directly connect
2. MongoDB version is too low
3. Too few shards
4. Underutilized SECONDARY node
5. Unarchiving historical cold data
6. The shard key is unreasonable, resulting in too many jumbo chunks
7. Improper use of statements, there are slow commands