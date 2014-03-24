---
layout: post
title: "Review: Learning Cypher"
date: 2014-08-30 21:35:39 -0500
comments: true
categories: [cypher, neo4j, nosql]
lang: en
---
I have had the change to review another book from **Packtpub.com**. Now, it's time to take a look inside the [Learning Cypher](https://www.packtpub.com/hardware-and-creative/learning-cypher).

Maybe you have heard about *NoSQL (Not only SQL)* databases. So, one kind is a `Graph Databases` and **Neo4j** is one of them, which is based on Nodes and Relationships.

**What is Cypher?** It is the Query Language used in Neo4j database.

It has a good introduction about Neo4j using embedded database and using the Java API provided by Neo4j.

For example: Imagine that we would like to get all the Users from the graph database. User must be an Node.

First, create an User node:
```
CREATE (a:User {username: "jroe", firstname: "Jane", lastname: "Roe"}),
(b:User {username: "cgarcia", firstname: "Carlos", lastname: "Garcia"}),
(c:User {username: "mweng", firstname: "Mei", lastname: "Weng"})
```

Using the query below you will get all the user information:
```
MATCH (u:User)
RETURN u
```

But, if we want some fields:
```
MATCH (u:User)
RETURN u.username, u.firstname, u.lastname
```

There are another example, using WHERE clause
```
MATCH (u:User)
WHERE u.username = 'cgarcia'
RETURN u
```

There are more topics using Regex, Join, Sorting and so on. Another interesting topics are:
* Profiling
* Migraton from SQL

**Note:** The author mention to *spring-data-neo4j* module from springframework which make the configuration and integration easy.

I really recommend this book if you want to dive into Neo4j world.
