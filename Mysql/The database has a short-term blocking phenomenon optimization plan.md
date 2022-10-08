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

### 1.4 queryTimeout

SQL statement execution timeout, tentatively set to 30 seconds (configuration tentative)

After configuring the parameters, the application service will start the backend thread before sending the sql statement to check whether the execution of mysql will time out

If the mysql execution exceeds the configured time, the backend thread will send the kill command, which will end the execution of the sql statement

```
<property name="queryTimeout" value="30" />
```

### 1.5 Upgrade mysql-connector to version 5.1.44 or later

```
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <version>5.1.44</version>
</dependency>
```

## 2. Increase the query data Redis cache
> When calling the interface, check the database directly every time

Construct multi-level cache, first cache locally, then redis cache, and finally check mysql

## 3. Optimizing slow SQL queries

Sort out all the slow queries of the slave library and export the EXCEL table

Distributed to each project leader for targeted optimization