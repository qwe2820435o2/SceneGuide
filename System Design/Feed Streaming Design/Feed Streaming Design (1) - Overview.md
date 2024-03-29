
# Overview

## 1. Push

```
Push is mainly used to push personalized feeds, and such feed messages will only trigger specified users

This method can optimize the user's feed performance, but it will occupy message storage resources

The scene is as follows:
Artist's new album release, follow, comment, application private message, etc.
```

## 2. Pull

```
Pull is mainly used for system-level feed related, such feed messages almost involve most users

This method can save more message storage resources, but it will be time-consuming for users to actively pull Feed messages, and it is also a test for interface performance

The scene is as follows:
System messages, user group messages, activity messages, etc.
```

## 3. Technology selection

```
The difficulty lies in the need to balance performance and resources

In view of this, we need to carefully evaluate the characteristics of each component and choose

CDN: Dynamic acceleration, intelligently select the best route back to the source for acquisition
Nginx: A reverse proxy server with excellent performance
Redis: Distributed cache with excellent performance and rich data types
Caffeine: A high-performance local cache
```

## 4. Architecture design

![Msg streaming design](../../Material/image/Msg%20streaming%20design.png)









