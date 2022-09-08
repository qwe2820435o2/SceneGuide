# Redis parameter normalization

| No   | Param    | Desc                                                         | Defaule | Suggest | Suggest Desc |
| ---- | -------- | ------------------------------------------------------------ | ------- | ------- | ------------ |
| 1    | maxTotal | The maximum number of connections in the connection pool, -1 means unlimited | 8       | 1500    |              |
| 2    | maxIdle  | The maximum number of idle connections allowed by the connection pool, excess idle connections will be released immediately | 8       | 500     |              |
| 3    | minIdle  | How many idle connections must be guaranteed in the connection pool, if not enough, new connections will be created | 0       | 50      |              |
| 4    |          |                                                              |         |         |              |