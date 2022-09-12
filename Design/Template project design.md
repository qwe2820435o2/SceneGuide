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


```

## 3. Structure Detail 

```

bp-template-server
├─bp-template-api       Jar Dependencies
   ├─model                  Model
   │  ├─dto                     data transfer object 
   │  ├─entity                  persistent object
   │  ├─qo                      query object
   │  ├─valid                   check object
   │  └─vo                      value object
   └─service                Interface
      ├─channel                 channel type interface
      ├─game                    game type interface
      └─manager             Management background interface
         ├─channel              channel type interface
         └─game                 game type interface

├─bp-template-common    Jar Dependencies
   ├─conmon                 Public constant
   │  ├─constans                constant type
   │  ├─enums                   enums type
   │  └─exception               exception type
   └─utils                  Tools

├─bp-template-dao       Jar Dependencies
   ├─manager                
   ├─dao                    
   ├─mapper                 
   └─model                  

```