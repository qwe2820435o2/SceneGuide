# Template project design

## 1. Project Instruction

- bp-template-server is a template parent-child project, which is vertically divided into 4 main modules and 3 sub-modules according to the business
- The four main modules, bp-template-bg, bp-template-service, bp-template-task, and bp-template-manager, are runnable jar package projects
- The three sub-modules, bp-template-api, bp-template-common, and bp-template-dao, are Jar package projects and provide dependencies for the main module
- Currently integrated components include: MySQL, Dubbo, RabbitMQ, Redis, MongoDB, Kafka, Apollo, XXL-JOB, Caffeine, etc

## 2. Whole Structure
> For each business service, modules can be selected for project construction according to the actual situation

```

Dependency Jar:

bp-template-api         (required)             Interface, model dependencies
bp-template-common      (optional)             Tools, constants dependencies
bp-template-dao         (optional)             Mapper dependencies

Runnable Jar:

bp-template-service     (required)             External interface service
bp-template-manager     (optional)             Management background interface service
bp-template-bg          (optional)             Asynchronous consumption service
bp-template-task        (optional)             Scheduled task service
bp-template-callback    (optional)             Third-party provider callback service


```

