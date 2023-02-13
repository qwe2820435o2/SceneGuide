# Structure Detail 



## 1. Common Dependent

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