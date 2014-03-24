---
layout: post
title: "Code Analysis with JArchitect"
date: 2015-05-27 00:02:29 -0500
comments: true
categories: [jarchitect, code analysis]
lang: en
---
Code Analysis is a really important stage in our projects, we need to take a look the software healthy every day. In this blog, `JArchitect` is the Code Analysis tool for Java projects that we are going to talk about.

Months ago I have the chance to get a JArchitect's license- thanks to the `CodeGears` team for this license. Then, I started taking a look how it works.

* Code Quality Metrics
* Graph Dependency
* Dependency Cycle

## Features
A really nice feature is that you can use `CQLinq` to build query over Java code. To learn more about `CQLinq` syntax check [here](http://www.jarchitect.com/Doc_CQLinq_Syntax). Also, allow you to create your own rules.

Modern projects use build tools to package their artifacts (jar, war, etc) So the integration with modern build tools such as `gradle` and `maven` is possible, you can follow the online documentation to set up.

* [Ant Integration](http://www.jarchitect.com/Doc_Ant)
* [Maven Integration](http://www.jarchitect.com/Doc_Maven)
* [Gradle Integration](http://www.jarchitect.com/Doc_Gradle)

Also, Continuous Integration process is real using JArchitect.

* [Jenkins Integration](http://www.jarchitect.com/Doc_CI_Jenkins)
* [TeamCity Integration](http://www.jarchitect.com/Doc_CI_TeamCity)

About `Code Coverage`, `cobertura` is the only technology supported by JArchitect at this moment. These metrics can be getting from xml files, but we need to generate reports previous to the code analysis.

Another great integration is that we can enrich our analysis with existing tools in the market like `CheckStyle`, `FindBugs`, `PMD`.

Languages that already run in the JVM can be analyze by JArchitect like `scala`, `groovy`, `clojure`.

For `Open Source` contributor there are good news. You can get your own free copy of `JArchitect`. How to apply? Check this [link](http://www.jarchitect.com/JArchitectForOSS) for more information. 

Analysis Bar![](https://dl.dropboxusercontent.com/u/15671111/blog/jarchitect%20-%20analysis.png)

Graph Dependency![](https://dl.dropboxusercontent.com/u/15671111/blog/jarchitect%20-%20graph%20dependency.png)

Report- Metrics![](https://dl.dropboxusercontent.com/u/15671111/blog/jarchitect%20-%20metrics.png)

Report- Rules Violated![](https://dl.dropboxusercontent.com/u/15671111/blog/jarchitect%20-%20rules%20violated.png)

CQLinq sentence![](https://dl.dropboxusercontent.com/u/15671111/blog/jarchitect-%20cqlinq.png)
