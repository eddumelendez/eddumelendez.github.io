---
layout: post
title: "How to start with Mule ESB"
date: 2014-12-31 20:22:57 -0500
comments: true
categories: [mule, maven, gradle]
lang: en
---
## What is an ESB?
It's a software architecture. ESB or Enterprise Service Bus is a Enterprise Integration Pattern (EIP) solves the `spaghetti integration` pattern.

## What is Mule ESB?
It is a Open Source Enterprise Service Bus (ESB), which allow to integrate lot of technologies.

Mule main parts:

- Component
- Transport
- Transformers
- Inbound/Outbound Routers

Mule also provide rich set of:

- Routers
- Transformers
- Filters

## Using Maven

Make sure you have set the Mulesoft's repository in `settings.xml`

```xml
<repositories>
  <repository>
    <id>mulesoft-release</id>
    <name>Mulesoft Release Repository</name>
    <url>https://repository.mulesoft.org/nexus/content/repositories/public/</url>
  </repository>
</repositories>
```

Also, check you have the pluginGroup `org.mule.tools`.

Now, you are able to run the following command your terminal:

```
mvn mule-project-archetype:create -DartifactId=helloWorld -DmuleVersion=3.5.0
```

## Using Gradle

Make sure you have a build.gradle file inside the folder with the following content:

```
buildscript {
    dependencies {
        classpath group: 'org.mulesoft.build', name: 'mule-gradle-plugin', version: '1.1.0'
    }

    repositories {
        maven {
            url 'http://repository.mulesoft.org/releases'
        }
    }
}

apply plugin: 'mule'

mule.version = '3.5.0'

mule.muleEnterprise = false
```

After that you can execute:

```
gradle initMuleProject
```

By default, `mule.muleEnterprise` is set to `true`.

For more information you can visit [mule-gradle-plguin](https://github.com/mulesoft-labs/mule-gradle-plugin) documentation.

Using maven or gradle you will be able to see the project like this

![](https://dl.dropboxusercontent.com/u/15671111/blog/mule-gradle.png)

## Differences between maven and gradle plugin

| Maven        | Gradle      |
| -------------|-------------|
| Provide `mule` packaging      | Provide `mule` plugin
| Allow to deploy in local mule standalone | Allow to deploy in local mule standalone, Mule Management Console and Cloudhub
|-|Allow to run application with a simple command

# Testing

`mule-config.xml` is placed inside of `src/main/app`. Here you will find a http service which will return `Hello World!` message.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- created by the gradle mule plugin -->

<mule xmlns:http="http://www.mulesoft.org/schema/mule/http" xmlns="http://www.mulesoft.org/schema/mule/core" xmlns:doc="http://www.mulesoft.org/schema/mule/documentation" xmlns:spring="http://www.springframework.org/schema/beans" version="EE-3.4.2" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-current.xsd
  http://www.mulesoft.org/schema/mule/core http://www.mulesoft.org/schema/mule/core/current/mule.xsd
  http://www.mulesoft.org/schema/mule/http http://www.mulesoft.org/schema/mule/http/current/mule-http.xsd">
  <flow name="mule-configFlow1" doc:name="mule-configFlow1">
    <http:inbound-endpoint exchange-pattern="request-response" host="localhost" port="8081" doc:name="HTTP"/>
    <set-payload doc:name="Set Payload" value="Hello World!"/>
  </flow>
</mule>
```

Then, proceed to write a test for the existing flow. As you can see response will be validated.

```java
import org.hamcrest.core.Is;
import org.junit.Assert;
import org.junit.Test;
import org.mule.api.MuleMessage;
import org.mule.api.client.MuleClient;
import org.mule.tck.junit4.FunctionalTestCase;

public class MuleTest extends FunctionalTestCase {

  @Override
  protected String getConfigFile() {
    return "src/main/app/mule-config.xml";
  }

  @Test
  public void testMuleConfigFlow1() throws Exception {
    MuleClient client = muleContext.getClient();
    MuleMessage message = client.request("http://localhost:8081", 3000L);
    String payload = message.getPayloadAsString();
    Assert.assertThat(payload, Is.is("Hello World!"));
  }
}

```
