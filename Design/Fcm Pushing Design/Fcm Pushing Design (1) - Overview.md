# Overview

```
FCM is a cross-platform messaging solution from google that allows us to reliably deliver messages at no cost

We usually push news about popular events and new albums to users, all of which require the use of FCM
```

**There are two ways to push FCM：**

1. Send To A Device Group
2. Send To Topic

### 1. Send To A Device Group
**Pros：**
```
The sending result of each batch of tokens can be obtained, which is convenient for statistical analysis
```


**Cons：**
```
1. Each batch can only process 500 tokens
2. We need to assume the responsibility of pushing, which will consume more resources
```



### 2. Send To Topic
**Pros：**
```
There is no need to assume the push responsibility, just need to maintain the relationship between the Topic and the token, and tell Google which Topic to push to, and Google will push it
```


**Cons：**