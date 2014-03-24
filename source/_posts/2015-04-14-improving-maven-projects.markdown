---
layout: post
title: "Improving maven projects"
date: 2015-04-14 22:17:16 -0500
comments: true
categories: [maven, maven-plugins, takari]
---
During long time **maven** has been the defacto build tool and dependency management for java projects. Since previous version some cool things has been added by plugins but now maven has been enriched with new features learning from the others.

* [Maven Lifecycle](#lifecycle)
* [Maven Polyglot](#polyglot)
* [Maven Wrapper](#wrapper)

All these new stuff is thanks to [Takiri](http://takari.io/) which is lead by Jason van Zyl ([@jvanzyl](https://twitter.com/jvanzyl)) the maven's father.

Requirements:

* Maven 3.3.1
* Java 7

<a name="lifecycle"></a>
## Maven Lifecycle
Avoid the re-compilation if there are no changes in the source code. Just is needed two simple steps to enable this awesome feature. Save your time!!!

**1.** Add plugin below:

```xml
<build>
  <plugins>
    <plugin>
      <groupId>io.takari.maven.plugins</groupId>
      <artifactId>takari-lifecycle-plugin</artifactId>
      <extensions>true</extensions>
    </plugin>
  </plugins>
</build>
```

**2.** Switch your current `packaging` from `jar` to `takari-jar`.

You can see the log to see if the plugin take effect. If you have compiled previously and you do again with after these configuration then no compilation will be done but if there are any change in your source code then it will compile again.

<a name="polyglot"></a>
## Maven Polyglot
Build `pom` file in xml format is verbose. Now, you can build your pom in different languages: atom, clojure, groovy, ruby, scala, yaml. And take advantage of each one.

Pre-requisite:

1. Inside the project create `.mvn/extensions.xml` file, where language dependency will take place:

### Atom

```xml
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
	<extension>
		<groupId>io.takari.polyglot</groupId>
		<artifactId>polyglot-atom</artifactId>
		<version>0.1.6</version>
	</extension>
</extensions>
```

### Clojure:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
	<extension>
		<groupId>io.takari.polyglot</groupId>
		<artifactId>polyglot-clojure</artifactId>
		<version>0.1.6</version>
	</extension>
</extensions>
```

### Groovy

```xml
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
  <extension>
		<groupId>io.takari.polyglot</groupId>
		<artifactId>polyglot-groovy</artifactId>
		<version>0.1.6</version>
	</extension>
</extensions>
```

### Ruby

```xml
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
	<extension>
		<groupId>io.takari.polyglot</groupId>
		<artifactId>polyglot-ruby</artifactId>
		<version>0.1.6</version>
	</extension>
</extensions>
```

### Scala

```xml
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
	<extension>
		<groupId>io.takari.polyglot</groupId>
		<artifactId>polyglot-scala</artifactId>
		<version>0.1.6</version>
	</extension>
</extensions>
```

### Yaml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<extensions>
	<extension>
		<groupId>io.takari.polyglot</groupId>
		<artifactId>polyglot-yaml</artifactId>
		<version>0.1.6</version>
	</extension>
</extensions>
```

Would you like to migrate your xml to any other language? You can do it running the command below:

```
mvn io.takari.polyglot:polyglot-translate-plugin:translate -Dinput=pom.xml -Doutput=pom.{format}
```

Where `format` could be `atom`, `clj`, `groovy`, `rb`, `scala` and `yml`.

<a name="wrapper"></a>
## Maven Wrapper
Share projects is common and sometimes we have specific version from our build tool. Now, you don't need to ask to your friend which maven version you need if the maven project use `maven-wrapper`. To do that, you just need to run:

```
mvn -N io.takari:maven:wrapper
```

Now you can make a build `mvnw clean install`. If you like to see which maven version you will download take a look at `.mvn/wrapper/maven-wrapper.properties` inside your project.
