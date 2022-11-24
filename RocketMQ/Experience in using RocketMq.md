# Experience in using RocketMq

## 1. Basic concept

### 1.1 Produce

Message producer, responsible for generating messages, generally the business system is responsible for generating messages

### 1.2 Consumer

Message consumer, responsible for consuming messages, generally the background system is responsible for asynchronous consumption

### 1.3 Push Consumer

Consumer的一种，应用通常向Consumer对象注册一个Listener接口，一旦收到消息，Consumer对象立刻回调Listener接口方法