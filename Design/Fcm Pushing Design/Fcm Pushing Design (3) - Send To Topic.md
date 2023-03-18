# Send To Topic
> Based on a publish/subscribe model, FCM topic messaging allows you to send messages to multiple devices that have opted into a specific topic

## 1. Sending Process

### 1.1 Preheating Topic Data

![Fcm Pushing Design (3) - Preheating Topic Data](../../Material/image/Fcm%20Pushing%20Design%20(3)%20-%20Preheating%20Topic%20Data.png)

### 1.2 Sending The Data Of Topics

![Fcm Pushing Design (3) - Sending The Data Of Topics](../../Material/image/Fcm%20Pushing%20Design%20(3)%20-%20Sending%20The%20Data%20Of%20Topics.png)

## 2. Optimize Direction

### 2.1 Data Query

```
Same as Data Query in FCM Pushing Design (3) - Send To A Device Group.md
```

### 2.2 Bind Topic

```
Batch binding Topic in the consumption logic, the maximum size can support a batch of 1000
```

### 2.3 Splite Topic
