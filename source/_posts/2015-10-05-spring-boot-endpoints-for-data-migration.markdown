---
layout: post
title: "Spring Boot Endpoints for Data Migration"
date: 2015-10-05 00:10:00 -0500
comments: true
categories: [spring-boot, flyway, liquibase]
---
Database Change Management has been one of the practices which I have not seen much in action but there is a first time for everything. When I started a new project time ago, I was aware of lack of this practice and the risks around. In order to avoid risks in the database and wasting time between team members with backups and restores, I started with the research. During the research, I met `Flyway` and `Liquibase`. Both are powerful but `liquibase` was chosen because meet the needs. You can read my post about [Database Change Management](http://eddumelendez.github.io/blog/2014/03/27/database-change-management/) and [Database Change Management with Liquibase](http://eddumelendez.github.io/blog/2014/08/11/database-change-management-liquibase/).

Currently, `Flyway` and `Liquibase` are supported by `spring-boot`. Both help to manage the scripts execution over the database and you can configure using `flyway.*` and `liquibase.*` property namespaces. Since version 1.3.0, endpoints for both technologies has been added, their purpose is display data in  `schema_version`, `databasechangelog` or any table you have customized. Previous to this change, credentials are required to access to the database in order to know this status. Now, everything is exposed via `spring-boot` and can be accessed to this information through the following endpoints `/flyway`, `/liquibase`.

These new endpoints have arrived thanks to `actuator` which provide several useful endpoints in `spring-boot`.

If you are currently using one of these technologies integrated with `spring-boot` you just need to add the actuator in your dependencies and voilá you can see through the inside.

For maven users:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-actuator</artifactId>
</dependency>
```

For gradle users:
```
org.springframework.boot:spring-boot-actuator
```

## /flyway endpoint

Once you have everything configure, point to the endpoint. E.g: http://localhost:8080/flyway

```json
[  
   {  
      "type":"SQL",
      "checksum":710039845,
      "version":"1",
      "description":"init",
      "script":"V1__init.sql",
      "state":"SUCCESS",
      "installedOn":1441826719448,
      "executionTime":3
   }
]
```

## /liquibase endpoint

Once you have everything configure, point to the endpoint. E.g: http://localhost:8080/liquibase

```json
[  
   {  
      "ID":"1",
      "AUTHOR":"marceloverdijk",
      "FILENAME":"classpath:/db/changelog/db.changelog-master.yaml",
      "DATEEXECUTED":1441826872659,
      "ORDEREXECUTED":1,
      "EXECTYPE":"EXECUTED",
      "MD5SUM":"7:b8f2ae9c88deabd32666dff9bc5d7f5d",
      "DESCRIPTION":"createTable",
      "COMMENTS":"",
      "TAG":null,
      "LIQUIBASE":"3.4.1",
      "CONTEXTS":null,
      "LABELS":null
   },
   {  
      "ID":"2",
      "AUTHOR":"marceloverdijk",
      "FILENAME":"classpath:/db/changelog/db.changelog-master.yaml",
      "DATEEXECUTED":1441826872663,
      "ORDEREXECUTED":2,
      "EXECTYPE":"EXECUTED",
      "MD5SUM":"7:a8006415097ebb8b3334a23347847322",
      "DESCRIPTION":"insert",
      "COMMENTS":"",
      "TAG":null,
      "LIQUIBASE":"3.4.1",
      "CONTEXTS":null,
      "LABELS":null
   }
]
```
