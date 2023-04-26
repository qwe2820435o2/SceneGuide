# Generate Msg

## 1. Overview

```
The service provides an RPC interface for sending messages

When the upstream service performs business operations, it uniformly calls this interface to send messages

Messages will be stuffed into different Redis Lists according to different business types
```

## 2. Process


![Counting Design (2) - Asynchronous Processing](../../Material/image/Feed%20Streaming%20Design%20(2)%20-%20Process.png)

## 3. Implementation Details

### 3.1 Trigger Time

```
Triggered by a specific function sent to you

Such as: invite registration, follow users, start activities, Buzz likes, etc.
```

### 3.2 Message Body

```
{
    "commonParams":{
        "refer":"xxx", //This parameter determines which message business processing queue to go
        "sentDate":"2023-02-09 12:00:00",
        "imei":"89fc9bcffcb84959",
        "imsi":"4ac123bcb615a5dc",
        "countryCode":"NG",
        "channel":"android-go"
    },
	"data":{
		"msgID":2345678945643514,
		"userId":5231792,
		...
	},
}
```

### 3.3 Asynchronous Processing

Send the message to RabbitMQ, which will be processed by consumers asynchronously and multi-threaded


