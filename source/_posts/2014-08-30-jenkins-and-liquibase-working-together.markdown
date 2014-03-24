---
layout: post
title: "Jenkins and Liquibase working together"
date: 2014-08-30 02:03:53 -0500
comments: true
categories: [cloudbees, jenkins, liquibase, maven]
lang: en
---
I have talked about [Database Change Management using Liquibase](http://eddumelendez.github.io/blog/2014/08/11/database-change-management-liquibase).
Now, I will talk about the integration with Jenkins CI.

As you can see in the example of my previous post. In the `pom.xml` there are 3 profiles: `update`,`tag` and `rollback` which will be used by Jenkins.
The profile approach will be useful in our integration.

I am going to use **Cloudbees** (PaaS)

**1.** First, you need to have an [Cloudbees](http://www.cloudbees.com/) account.  

**2.** Click on *Databases* and then click *Add Database*.  

**3.** Create a liquibase_demo database.

**4.** Click on *Builds*, Jenkins dashboard will be display.

**5.** Create *New Job*.

**6.** Put a name, choose *Build a free-style software project* option and then click *OK*.

**7.** Now, let start to configure Jenkins's job. You will be able to see the image below
  ![](https://dl.dropboxusercontent.com/u/15671111/blog/liquibase-jenkins-1.png)

**8.** Check *This build is parameterized* option. Then, click *Add Parameter*. Add the following parameters: `driver`, `url`, `username`, `password`, `changeLogFile`, `tag` and `action`.

  `driver`, `url`, `username`, `changeLogFile`, `tag` are **String Parameter**
  ![](https://dl.dropboxusercontent.com/u/15671111/blog/liquibase-jenkins-2.png)

  `password` is a **Password Parameter**.
  ![](https://dl.dropboxusercontent.com/u/15671111/blog/liquibase-jenkins-3.png)

  `action` is a **Choice Parameter** with the following options: `update`, `tag` and `rollback`
  ![](https://dl.dropboxusercontent.com/u/15671111/blog/liquibase-jenkins-4.png)

**9.** Now, lets configure the Source Code Management. In this example, I have published the [demo](https://github.com/eddumelendez/liquibase-demo) in GitHub.
  ![](https://dl.dropboxusercontent.com/u/15671111/blog/liquibase-jenkins-5.png)

**10.** Now, go to **Build** section, click on *Add build step* and choose *Invoke top-level Maven targets*. Add the maven's goal and properties. Then, *Save*.

Maven Goal:

```
mvn install -P$action
```

Maven Properties:

```
liquibase.driver=$driver
liquibase.username=$username
liquibase.password=$password
liquibase.url=$url
liquibase.changeLogFile=$changeLogFile
liquibase.rollbackTag=$tag
liquibase.tag=$tag
liquibase.promptOnNonLocalDatabase=false
```

  If you remember, we have created parameters at the beginning of this post which are reusing in this part using `$` in order to do a dynamic job.
  ![](https://dl.dropboxusercontent.com/u/15671111/blog/liquibase-jenkins-6.png)

**11.** Finally, click *Build with parameters*, test your job and enjoy.
  ![](https://dl.dropboxusercontent.com/u/15671111/blog/liquibase-jenkins-7.png)

Avoid risks and say good bye to manual tasks. For that reason, I love automation!

**Note:** Liquibase can be used inside the java application using [spring integration](http://www.liquibase.org/documentation/spring.html).
