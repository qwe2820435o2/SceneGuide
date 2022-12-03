# Experience in using RocketMq

## 1. Basic concept

### 1.1 Produce

Message producer, responsible for generating messages, generally the business system is responsible for generating messages

### 1.2 Consumer

Message consumer, responsible for consuming messages, generally the background system is responsible for asynchronous consumption

### 1.3 Push Consumer

A type of Consumer. Applications usually register a Listener interface with the Consumer object. Once a message is received, the Consumer object immediately calls back the Listener interface method.

### 1.4 Pull Consumer

A type of Consumer, the application usually actively calls the Consumer's pull message method to pull messages from the Broker, and the initiative is controlled by the application

### 1.5 ProducerGroup

The collection name of a type of Producer, this type of Producer usually sends a type of message, and the sending logic is consistent

### 1.6 Consumer Group

The collection name of a type of Consumer. This type of Consumer usually consumes a type of message, and the consumption logic is consistent

### 1.7 Broker

Message relay role, responsible for storing and forwarding messages, also known as Server

### 1.8 NameService

Responsible for routing, management

### 1.9 Broadcast consumption

A message is consumed by multiple consumers

Even if these Consumers belong to the same Consumer Group, the message will be consumed once by each Consumer in the Consumer Group

The Consumer Group concept in broadcast consumption can be considered meaningless in terms of message division

### 1.10 Cluster consumption

Consumer instances in a Consumer Group share consumption messages evenly

For example, a Topic has 9 messages, and a Consumer Group has 3 instances

Then each instance only consumes 3 of the messages


**Consumption patterns:**

![Cluster consumption](../Material/image/Experience%20in%20using%20RocketMq%20—%20Cluster%20consumption.png)

**Deploy patterns:**

![Deploy patterns](../Material/image/Experience%20in%20using%20RocketMq%20—%20deploy%20consumption.png)

## 2. Summary of Production Problems

```markdown
1. Under the same topic in different jvms, the tag subscriptions are inconsistent, resulting in inconsistent message status and consumption congestion
2. The topic subscriptions of consumers under the same consumer group are inconsistent, resulting in inconsistent message status and consumption congestion
3. After a certain consumer goes offline, the offline status is not synchronized with the entire cluster
4. There is no consumer registration under a certain broker
5. The network is unstable or the consumer is restarted, and the message is repeatedly consumed
```

## 3. Summary of production experience

### 3.1 Issue

The most common problems in production are: inconsistent message status, which leads to message squeeze, such as the two problems a and b mentioned above

### 3.2 Solution

```markdown
Multiple Consumers are started in different JVMs, and different Topics are configured for the same Consumer ID
```