# Feed Pull

## 1. Overview

```
Pull is mainly used for system-level feed related, such feed messages almost involve most users

This method can save more message storage resources, but it will be time-consuming for users to actively pull Feed messages, and it is also a test for interface performance

If the amount of data here is not large, you can introduce local cache to optimize performance

The scene is as follows:
System messages, user group messages, activity messages, etc.
```

## 2. Process

```mermaid
graph LR
A(User)  --> B[Service: Get Msg]
B[Service: Get Msg] -- Query Content & Cut Out MMsg --> C((Redis List))
B[Service: Get Msg] -- Complete Details --> D((Local Cache))
D((Local Cache))  --> C((Redis List))
D((Local Cache))  --> E((MYSQL))
```

## 3. Details

### 3.1 General Parameter

**REQ:**

```
userId				// User ID
imei				// Equipment Identity
imsi				// Equipment Identity
countryCode			// Country Code	
channel				// Channel	
maxUserMsgId		// The maximum msgId of the current user message
maxDeviceMsgId		// The maximum msgId of the current device message
```

### 3.2 General Response

**RESP:**

```
maxUserMsgId					// The maximum msgId of the current user message	
maxDeviceMsgId					// The maximum msgId of the current device message

List<PullMessage> msgList
	msgId						// Message Id	
	msgType						// Message Type
	timestamp					// timestamp
	userId						// User Id
	content						// Message Content
```

### 3.3 Get User Information

```mermaid
graph LR
A[get maxUserMsgId from Redis] --> B[get user message from Redis]
B[get user messages from Redis] --> C[filter read messages based on maxUserMsgId]
C[Filter read messages based on maxUserMsgId] --> D[Complete complete messages based on entity Id]
D[Complete the complete message according to the entity Id] --> E[Update maxUserMsgId & return]
```

### 3.3 Get System Information

```mermaid
graph LR
A[Get maxDeviceMsgId from Redis] --> B[Get device information from Redis according to imei&country]
B[get device messages from Redis according to imei&country] --> C[filter read messages according to maxDeviceMsgId]
C[Filter read messages based on maxDeviceMsgId] --> D[Complete complete messages based on entity Id]
D[Complete the complete message according to the entity Id] --> E[Update maxDeviceMsgId & return]
```