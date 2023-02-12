# Feed Push

## 1. Overview

```
Push is mainly used to push personalized feeds, and such feed messages will only trigger specified users

The scene is as follows:
Artist's new album release, follow, comment, application private message, etc.

Middleware: Redis, data structure: List

Users have their own exclusive message list, specific scenarios such as: entering the home page, entering the personal center, etc

Trigger the message pull operation of the user message list
```


## 2. Process

```mermaid
graph LR
A((RabbitMQ Queue)) -- consume --> B[Service: Handling Msg]
B[Service: Handling Msg] -- call --> C[Send To Redis]
C --> D((Redis List))
E(User) -- get --> D((Redis List))
```

## 3. Details
### 3.1 Push Timing

```
The scene is as follows:
Artist's new album release, follow, comment, application private message, etc.

Insert the corresponding user's message into the Redis List
```

### 3.2 Data Structure

```
The currently selected data structure for storing user messages is: Redis List

However, after actual use, it is still not the best in terms of memory utilization and ease of use

Regarding the selection of data structures, we will discuss in detail in Feed streaming design (5) - Subsequent Optimization
```