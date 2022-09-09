# Mysql parameter normalization

| No   | Param                         | Desc                                                         | Defaule | Suggest  | Suggest Desc                                                 |
| ---- | ----------------------------- | ------------------------------------------------------------ | ------- | -------- | ------------------------------------------------------------ |
| 1    | maxActive                     | The maximum number of active connections that the connection pool can allocate at the same time | 100     | 300      |                                                              |
| 2    | maxIdle                       | "The maximum number of connections to always keep in the pool, if enabled, limit connections will be checked periodically, Connections that exceed the value set by this property and the idle time exceeds minEvictableIdleTimeMillis will be released" | 100     | 300      |                                                              |
| 3    | minIdle                       | "Always keep the minimum number of connections in the pool. If the number of connections in the pool is lower than this value, a new connection will be created. Narrows down to this value if connection validation fails" | 100     | 100      |                                                              |
| 4    | initialSize                   | The initial number of connections created when the connection pool starts | 10      | 10       |                                                              |
