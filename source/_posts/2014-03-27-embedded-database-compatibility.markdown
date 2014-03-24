---
layout: post
title: "Embedded Database compatibility"
date: 2014-03-27 22:01:18 -0500
comments: true
categories: [hsql, h2, database, maven]
lang: en
---

Some weeks ago I was watching a video about [Spring Testing](https://www.youtube.com/watch?v=LYVJ69h76nw), one thing that called my attention was one feature about embedded databases. It is about compatibility with other databases.

From my side, this feature is really useful because when I started using embedded database in my tests I had to change some types or remove lines in my script due to there are not supported (At that time, I didn't know about it)

Lines below you can see how to setup **MYSQL** compatibility into **HSQL** and **H2** databases, both for testing purpose. Also, you can see the dependencies if you are using maven projects.

## HSQL
You can review this [link](http://hsqldb.org/doc/guide/dbproperties-chapt.html) for more information.

{% codeblock lang:sql script.sql%}
SET DATABASE SQL SYNTAX MYS TRUE;
{% endcodeblock %}

{% codeblock lang:xml+evoque pom.xml%}
<dependency>
	<groupId>org.hsqldb</groupId>
	<artifactId>hsqldb</artifactId>
	<version>2.2.8</version>
	<scope>test</scope>
</dependency>
{% endcodeblock %}

## H2
You can review this [link](http://www.h2database.com/html/features.html#compatibility) for more information.

{% codeblock lang:sql script.sql%}
SET MODE MySQL;
{% endcodeblock %}

{% codeblock lang:xml+evoque pom.xml%}
<dependency>
	<groupId>com.h2database</groupId>
	<artifactId>h2</artifactId>
	<version>1.3.175</version>
	<scope>test</scope>
</dependency>
{% endcodeblock %}
