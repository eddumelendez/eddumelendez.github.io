---
layout: post
title: "database change management"
date: 2014-03-27 22:15:11 -0500
comments: true
categories: [liquibase, flyway, dbdeploy, automation]
lang: en
---
First, I have some questions to you:

1. Do you have scripts into the Source Control Management?
2. Do you know which scripts have been executed into the database?
3. Do you write scripts for rollback?
4. Are DBAs involve in your development process?
5. Tell me, how do you manage your database changes?

If I were a new team member, I will ask you how to build my database and maybe this would be your answer "Let me get a dump from my local database and I will send you". This is valid if your dump has the same structure that production environment but I would not be 100% sure.
Another option is get a backup from production, is not a bad idea if you want to work with real data and solve a specific issue but is not ever the case. So, you must be able to build the database whenever you want.

## What it is my point?
Continuous Improvement, that is my point. We need to improve our delivery process every day and Database Change Management is something that you can not forget.

## Which is involve?
1. Every database modification should be written as a delta script.
2. Add rollback section to your scripts.
3. Use a naming conventions for your scripts.
4. If a delta script has already been applied to a database is subsequently modified that subsequent modification will not be applied to the database.
5. Version Control your scripts.
6. Maintain a database changelog.

## Advantages
1. Reduce risks during deployments.
2. Ensure you are executing the right scripts.
3. You can build a new database.

After this, you can research about some tools such as [liquibase](http://www.liquibase.org/) or [flyway](http://flywaydb.org/) in order to automated scripts execution and then promote communication with Database Team in your job.
