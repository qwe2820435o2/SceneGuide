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