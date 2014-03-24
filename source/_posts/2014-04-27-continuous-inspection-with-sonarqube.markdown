---
layout: post
title: "Continuous Inspection with SonarQube"
date: 2014-04-27 23:28:37 -0500
comments: true
categories: [sonar, sonarqube, continuous inspection]
lang: en
---
## What is Continuous Inspection?
It is an Agile Practice which tell us inspect the source code in order to find bad habits avoiding issues and bad design in the future.

## What is SonarQube?
[SonarQube](http://www.sonarqube.org/) is an Open Source Project based on seven axes of quality:

1. Potential bugs
2. Coding rules
3. Tests
4. Duplications
5. Comments
6. Architecture and design
7. Complexity

Sonar (the firstname of this project) or SonarQube (current name) help us to identify points mentioned above.

#### Did you remember this phrase?
>Loose coupling and high cohesion.

Into the dashboard, you can see RFC (Response For Class) and LCOM4 (Lack of Cohesion Of Methods version 4). Those are related to Coupling and Cohesion respectively.

![](https://dl.dropboxusercontent.com/u/15671111/blog/sonarqube-RFC.png)

![](https://dl.dropboxusercontent.com/u/15671111/blog/sonarqube-LCOM4.png)

**Code Review** and **Pair Programming** are practices that we need to do in order to support Continuous Inspection Process.
