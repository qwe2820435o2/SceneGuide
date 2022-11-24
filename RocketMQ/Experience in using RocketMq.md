# Experience in using RocketMq

## 1. Basic concept

### 1.1 Produce

Message producer, responsible for generating messages, generally the business system is responsible for generating messages

### 1.2 Consumer

Message consumer, responsible for consuming messages, generally the background system is responsible for asynchronous consumption

### 1.3 Push Consumer

A type of Consumer. Applications usually register a Listener interface with the Consumer object. Once a message is received, the Consumer object immediately calls back the Listener interface method.