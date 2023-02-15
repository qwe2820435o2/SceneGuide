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
channel				// channel	
maxUserMsgId		// The maximum msgId of the current user message
maxDeviceMsgId		// The maximum msgId of the current device message
```

### 3.2 General Response

**RESP:**

```
maxUserMsgId					// The maximum msgId of the current user message	
maxDeviceMsgId					// The maximum msgId of the current device message


```