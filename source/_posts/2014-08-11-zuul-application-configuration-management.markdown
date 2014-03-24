---
layout: post
title: "Zuul: Application Configuration Management"
date: 2014-08-11 01:23:06 -0500
comments: true
categories: [zuul, maven, java, spring]
lang: en
---

Months ago I read the following blog **Mule Meets Zuul** [Part I](http://blogs.mulesoft.org/mule-meets-zuul-centralized-properties-management-part-1/) | [Part II](http://blogs.mulesoft.org/mule-meets-zuul-centralized-properties-management-part-2/) at [Mulesoft's blog](http://blogs.mulesoft.org)
and Zuul caught my attention.

## What is the problem?
It is a headache when you have to lead with a lot of property files and even worst when you have many environments.

## What is Zuul?
Zuul is an open source web application which centralize and manage property files configuration.

## What can I do?

* Create environments
* Upload property files
* Create new entries
* Clone property files between environments
* Group property files in folders
* Encryption support

## Steps to install Zuul
Zuul can integrate with Google, Yahoo, LDAP and Active Directory.

Here the steps to set up Zuul against LDAP.

**1.** Install [OpenLDAP](http://docs.adaptivecomputing.com/viewpoint/hpc/Content/topics/1-setup/installSetup/settingUpOpenLDAPOnCentos6.htm).

**2.** Load this [file](https://dl.dropboxusercontent.com/u/15671111/blog/ldap-data.ldif) into the LDAP.

**3.** Instal Mysql

```
yum install-y mysql-server mysql-devel
chkconfig mysqld on
service mysqld start
```

**4.** Create zuul database.

**5.** Download  [Zuul](http://www.devnull.org/zuul).

**6.** Set this parameters at:

   **Unix:** %TOMCAT_HOME%/bin/catalina.sh

```
export JAVA_OPTS=-Dspring.profiles.active="security-ldap"
```

   **Windows:** %TOMCAT_HOME%/bin/catalina.bat

```
set JAVA_OPTS=-Dspring.profiles.active="security-ldap"
```

**7.** Add database driver into **%TOMCAT_HOME%/lib**.

**8.** Copy ldap.properties and zuul-data-config.properties from **zuul/WEB-INF/classes/examples** to **%TOMCAT_HOME%/lib**.

**9.** Modify ldap.properties
{% codeblock lang:properties ldap.properties%}
ldap.url=ldap://localhost:389
ldap.username=cn=Manager,dc=example,dc=com
ldap.password=p@ssw0rd
ldap.dn.ROLE_SYSTEM_ADMIN=CN=Zuul System Admins,OU=Groups,DC=acme,DC=com
ldap.dn.ROLE_ADMIN=CN=Zuul Admins,OU=Groups,DC=acme,DC=com
ldap.dn.ROLE_USER=CN=Zuul Users,OU=Groups,DC=acme,DC=com
ldap.group.search.base=OU=Groups,DC=acme,DC=com
ldap.group.role.attribute=entryDN
ldap.group.filter=member={0}
ldap.user.search.base=OU=Users,DC=acme,DC=com
ldap.user.search.filter=uid={0}
{% endcodeblock %}

**10.** Start tomcat and zuul application will create the database tables using [liquibase](http://www.liquibase.org).

Now, you have Zuul application ready to use.

Create a property in dev environment named **myproperty**

Download [Zuul demo](https://github.com/eddumelendez/zuul-demo)

Now run mvn test, you will get the value from Zuul Service.

## Screenshots
Create new property option.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-1.png)

Create new property view.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-2.png)

Property created.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-3.png)

Property view and ready to add key and values.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-4.png)

Adding new property.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-5.png)

Property created in DEV environment.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-6.png)

Key Management option.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-7.png)

Key Management view.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-8.png)

Changing password.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-9.png)

You can also create groups.
![](https://dl.dropboxusercontent.com/u/15671111/blog/zuul-10.png)
