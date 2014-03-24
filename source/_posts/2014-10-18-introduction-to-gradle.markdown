---
layout: post
title: "Introduction to Gradle"
date: 2014-10-18 08:57:01 -0500
comments: true
categories: [gradle]
lang: en
---
`Gradle` is called the next generation of **build automation** and **dependency management**. If you have used `Ant` or `Maven` you know what that mean.

`Gradle` is based on `Groovy` and has compatibility with existing tools like `Ant` and `Maven`.

The company behind this project is **Gradleware**.

###### Build Automation
As you know, manual tasks are error-prone and tedious. Take in mind that you are working in a project and you have to compile your code... manually!!! It's boring and you are spending time if you are doing this, Can you imaging running `javac` command for all your project and dependencies? and after that you need to package the artifact in a `jar` or `war`. `Ant` is the first tool which help developers to write a xml file with all the step to compile, copy, package artifacts. Currently, `Maven` have standardized all of this and it is charge of to run all the previous tasks and manage the dependencies.

###### Dependency Management
All the projects have dependencies with other projects, years ago and even now is a headache when you are copying and pasting jars inside your projects. To avoid this pain `maven` and `ivy` are tools to manage this.

## Getting Started

It is really cool to see what amazing things you can do with `Gradle`. It allow us to work with `java`, `groovy` and `scala` projects too.

I really like the easy way to add tasks and manage the dependencies between them. Another good thing is the capability to extend the functionality in `Java` or `Groovy`.

`Gradle` have the power run tasks in a new way: Gradle task name abbreviation. For example, if you have created a task called deployInLocalhost... run `gradle dIL` instead of`gradle deployInLocalhost` but make sure you have not another task with the same abbreviation.

## Gradle Wrapper

I remember when I started using `maven`, I had downloaded some examples but that was not enough. I had to install `maven` in my local machine. To avoid install new runtime manually like I did, Gradle Wrapper has arrived to the rescue!!!

As a best practice, it is a good idea to have a wrapper in your project in order to avoid compatibility troubles or any other issues. To apply the wrapper configuration you just need to execute this command **gradle wrapper** and changes to your project will be applied, your wrapper will have the same version as your gradle runtime but you can change it.

## Gradle Daemon

Gradle take time to up and run when task is executed. If you want to improve the performance, Gradle daemons is here to the rescue... to active it **gradle --daemon** and finalize the process **gradle --stop**. This is useful when you run unit test many times.

**Note:** expire after 3 hours.

## Moving from Maven to Gradle

Currently, you may are working with `maven` so if you want to try `gradle` without lost all your maven configuration you can run this command **gradle maven2gradle**. It will create the `build.gradle` and `settings.gradle` files with all the dependencies and configuration. Looks great, right? but as a new build automation tool, `gradle` is growing so if you have additional plugin configuration in your `pom.xml` this will not be migrated. Your project can live with both.

## Gradle Commands

I will describe some useful commands but to get more information visit [online documentation](http://www.gradle.org/docs/current/userguide/gradle_command_line.html).

All those commands start with `gradle`: `gradle <command>`

Commands:

**-v or --version** -> display gradle version.

**tasks** -> display tasks related to the project.

**-q** -> show tasks output.

**-x** or **gradle --exclude-task** -> exclude the execution of tasks defined.

**dependencies** -> display project dependencies and how dependencies were solved.

**projects** -> list all the project and subprojects.

**properties** -> list all available properties in the project.

**-a** or **--no-rebuild** -> it's used when you won't to rebuild a projects that you didn't change. It works if you are only changing files in a single project.

**--refresh-dependencies** -> refresh project dependencies.

**-b** or **--build-file** -> give the option to choose another build script.

**-Dtest.debug test** -> debug test in port 5005


## Recommended Books

* [Gradle in Action](http://www.manning.com/muschko/)
