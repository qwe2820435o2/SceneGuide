# The database has a short-term blocking phenomenon optimization plan
> Adding fields to a large table causes the database to be blocked for a short time, which in turn blocks the SQL query requests of the API's normal business, resulting in inaccessibility

## 1. Project Druid link pool configuration
> Note: waitTime and connectTimeout are configured first, queryTimeout and socketTimeout need to wait for the api slow query to be transformed and then enabled

### 1.1 waitTime

Get mysql connection wait time. Originally 10000 (10 seconds), modified to: 5000

```
<property name="maxWait" value="5000" />
```

### 1.2 connectTimeout

The default tcp connection establishment timeout time is 0, modified to: 5000

```
<property name="url" value="jdbc:mysql://10.116.55.1:3306/platform_user?characterEncoding=UTF-8&amp;connectTimeout=5000" />
```

### 1.3 socketTimeout

The client sends SQL statements and waits for the response time of the MySQL service. Defaults to 0 depending on the OS to time out after 30 minutes. Modify it to 40000 (the configuration is tentatively set for 40 seconds)

```
<property name="url" value="jdbc:mysql://10.116.55.1:3306/platform_user?characterEncoding=UTF-8&amp;socketTimeout=40000/>
```






