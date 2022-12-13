# Msg streaming design

## 1. Overview

### 1.1 Push

```
Push is mainly used to push personalized feeds, and such feed messages will only trigger specified users

This method can optimize the user's feed performance, but it will occupy message storage resources

The scene is as follows:
Artist's new album release, follow, comment, application private message, etc.
```

### 1.2 Pull

```
Pull is mainly used for system-level feed related, such feed messages almost involve most users

This method can save more message storage resources, but it will be time-consuming for users to actively pull Feed messages, and it is also a test for interface performance


```



