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
└─bp-template-api       Jar Dependencies
   ├─model                  Model
   │  ├─dto                     data transfer object 
   │  │  ├─req                      req dto
   │  │  ├─resp                     resp dto
   │  │  └─common                   common dto
   │  ├─po                      persistent object
   │  ├─qo                      query object
   │  ├─bo                      business object
   │  └─vo                      value object
   └─service                Interface
      ├─channel                 channel type interface
      ├─game                    game type interface
      └─manager             Management background interface
         ├─channel              channel type interface
         └─game                 game type interface

└─bp-template-common    Jar Dependencies
   ├─conmon                 Public constant
   │  ├─constans                constant type
   │  ├─enums                   enums type
   │  └─exception               exception type
   └─utils                  Tools

└─bp-template-dao       Jar Dependencies
   ├─manager                Redis, MongoDB operation related
   ├─dao                    Data aggregation, transformation related
   ├─mapper                 Mapper
   └─model                  Model



├─bp-template-service   External interface service
│  ├─Startup                Project startup class
│  ├─core                   Core module
│  │  ├─annotation              annotation
│  │  ├─aspect                  aspect
│  │  ├─config                  config
│  │  │  ├─kafka                    kafka config
│  │  │  ├─rabbitmq                 rabbitmq config
│  │  │  ├─redis                    redis config
│  │  │  └─root                     basic config
│  │  ├─exception               exception
│  │  ├─interceptor             interceptor
│  │  ├─mapper                  mapper
│  │  ├─cover                   vo,dto,entity,qo cover
│  │  ├─model                   model
│  │  └─utils                   tools
│  └─template               Business module
│     ├─cache                   cache operation 
│     ├─controller              provide app http interface
│     ├─dubbo                   provide app rpc interface 
│     ├─kafka                       kafka operation
│     │  └─producer                     producer operation
│     ├─manager                     rpc interface manager operation
│     ├─rabbit                      rabbit operation
│     │  └─producer                     producer operation
│     └─service                     service operation
└─resources                 Resource directory
   ├─application.yml            Project configuration
   └─logback-spring.xml         Log configuration



├─bp-template-manager   Management background interface service
│  ├─Startup                Project startup class
│  ├─core                   Core module
│  │  ├─annotation              annotation
│  │  ├─aspect                  aspect
│  │  ├─config                  config
│  │  │  ├─kafka                    kafka config
│  │  │  ├─rabbitmq                 rabbitmq config
│  │  │  ├─redis                    redis config
│  │  │  └─root                     basic config
│  │  ├─exception               exception
│  │  ├─interceptor             interceptor
│  │  ├─mapper                  mapper
│  │  ├─cover                   vo,dto,entity,qo cover
│  │  ├─model                   model
│  │  └─utils                   tools
│  └─template               Business module
│     ├─cache                   cache operation 
│     ├─controller              provide manager http interface
│     ├─dubbo                   provide manager rpc interface 
│     ├─kafka                       kafka operation
│     │  └─producer                     producer operation
│     ├─manager                     rpc interface manager operation
│     ├─rabbit                      rabbit operation
│     │  └─producer                     producer operation
│     └─service                     service operation
└─resources                 Resource directory
   ├─application.yml            Project configuration
   └─logback-spring.xml         Log configuration



├─bp-template-bg   Asynchronous consumption service
│  ├─Startup                Project startup class
│  ├─core                   Core module
│  │  ├─annotation              annotation
│  │  ├─aspect                  aspect
│  │  ├─config                  config
│  │  │  ├─kafka                    kafka config
│  │  │  ├─rabbitmq                 rabbitmq config
│  │  │  ├─redis                    redis config
│  │  │  └─root                     basic config
│  │  ├─exception               exception
│  │  ├─interceptor             interceptor
│  │  ├─mapper                  mapper
│  │  ├─cover                   vo,dto,entity,qo cover
│  │  ├─model                   model
│  │  └─utils                   tools
│  └─template               Business module
│     ├─cache                   cache operation 
│     ├─controller              provide app http interface
│     ├─dubbo                   provide app rpc interface 
│     ├─kafka                       kafka operation
│     │  ├─consumer                     consumer operation
│     │  └─producer                     producer operation
│     ├─manager                     rpc interface manager operation
│     ├─rabbit                      rabbit operation
│     │  ├─consumer                     consumer operation
│     │  └─producer                     producer operation
│     └─service                     service operation
└─resources                 Resource directory
   ├─application.yml            Project configuration
   └─logback-spring.xml         Log configuration



├─bp-template-task   Scheduled task service
│  ├─Startup                Project startup class
│  ├─core                   Core module
│  │  ├─annotation              annotation
│  │  ├─aspect                  aspect
│  │  ├─config                  config
│  │  │  ├─kafka                    kafka config
│  │  │  ├─rabbitmq                 rabbitmq config
│  │  │  ├─redis                    redis config
│  │  │  ├─task                     task config
│  │  │  └─root                     basic config
│  │  ├─exception               exception
│  │  ├─interceptor             interceptor
│  │  ├─mapper                  mapper
│  │  ├─cover                   vo,dto,entity,qo cover
│  │  ├─model                   model
│  │  └─utils                   tools
│  └─template               Business module
│     ├─cache                   cache operation 
│     ├─controller              provide app http interface
│     ├─dubbo                   provide app rpc interface 
│     ├─kafka                       kafka operation
│     │  └─producer                     producer operation
│     ├─manager                     rpc interface manager operation
│     ├─rabbit                      rabbit operation
│     │  └─producer                     producer operation
│     ├─service                     service operation
│     └─task                        task operation
└─resources                 Resource directory
   ├─application.yml            Project configuration
   └─logback-spring.xml         Log configuration

```