# Generate Msg

## 1. Overview

```
The service provides an RPC interface for sending messages

When the upstream service performs business operations, it uniformly calls this interface to send messages

Messages will be stuffed into different Redis Lists according to different business types
```

## 2. Process

```mermaid
graph LR
A[Buzz Service] -- call --> D((RabbitMQ))
B[OMS Service] -- call --> D((RabbitMQ))
C[Activity Service] -- call --> D[Send RPC Service]
D[Send RPC Service] -- send --> E((RabbitMQ Queue))
E -- Consume --> F[Service: Message Handling]
F[Service: Message Handling] -- call --> G[Data Analysis]
F[Service: Message Handling] -- call --> H[Data Assembly]
F[Service: Message Handling] -- call --> I[Send to Redis]
```