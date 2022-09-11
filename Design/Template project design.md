**Project Instruction** 

- bp-template-server is a template parent-child project, which is vertically divided into 4 main modules and 3 sub-modules according to the business
- The four main modules, bp-template-bg, bp-template-service, bp-template-task, and bp-template-manager, are runnable jar package projects
- The three sub-modules, bp-template-api, bp-template-common, and bp-template-dao, are Jar package projects and provide dependencies for the main module
- Currently integrated components include: MySQL, Dubbo, RabbitMQ, Redis, MongoDB, Kafka, Apollo, XXL-JOB, Caffeine, etc

**Project Structure** 

```

Dependency Jar:

bp-template-api             Interface, model dependencies
bp-template-common          Tools, constants dependencies
bp-template-dao             Mapper dependencies

Runnable Jar:

bp-template-service         External interface service
bp-template-manager         Management background interface service
bp-template-bg              Asynchronous consumption service
bp-template-task            Scheduled task service


```
