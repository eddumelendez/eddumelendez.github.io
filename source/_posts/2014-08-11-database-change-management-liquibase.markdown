---
layout: post
title: "Database Change Management: Liquibase"
date: 2014-08-11 14:23:31 -0500
comments: true
categories: [liquibase, ant, maven]
lang: en
---

Months ago, I published my first post about [Database Change Management](http://eddumelendez.github.io/blog/2014/03/27/database-change-management). So now, we will review [liquibase](http://www.liquibase.org).

In this blog, I am using sql scripts but there are another ways to work with Liquibase such as XML, YAML, JSON and you have to consider which it is the best option for you.

## What is Liquibase?
It is an open source project which help us to manage the scripts execution into the database avoiding headaches during the SDLC.

## How liquibase works?
First of all, you need to add the liquibase dependency and the database dependency (mysql in this post) into the pom.xml
After that, add scripts into the project. Then you must to register the script added into the liquibase configuration xml.

Take into account that if your script is not registered into the liquibase configuration xml, script will not be executed automatically.

Finally you can run the following maven goal **liquibase:update**, which will create two tables into the database. All the scripts executed against the database will be stored into the **databasechangelog** table.

## Pre-requisites
* Java
* Ant
* Maven

## Liquibase's Goals

I will mention just some of them, the list below are the most used by me:

* `rollback`: run all the scripts in the **rollback** section inside of dbchangelog configuration file.
* `tag`: mark the last script executed.
* `update`: run all the scripts in the **sqlFile** section inside of dbchangelog configuration file.
* `updateTestingRollback`: allow to test all the scripts. First, do the update and then rollback task. Make sure that all your scripts has a rollback section inside of dbchangelog configuration file. Otherwise, it doesn't work.

> **Note:** See all the liquibase's goals [here](http://www.liquibase.org/documentation/maven/).

## Demo
You can download the example [here](https://github.com/eddumelendez/liquibase-demo).

As you can see, there are **param.properties** which have the database connection and another values.

**1.** Lets explain some key properties:

**changeLogFile**, filename which contains scripts to be executed.

**tag**, the name of tag.

**2.** Run the ant task **mvn_liquibase_update**, it will create t_user table. Also, script executed will be registered into the **databasechangelog** table.

**3.** Now, lets change **changeLogFile** value into the **params.properties** by db.changelog-1.1.0.xml

**4.** Run the ant task **mvn_liquibase_update** again, it will create t_role table.

Now, the scripts execution can be automated using Jenkins.
