---
layout: post
title: "Spring 4.2.0: SpringClassRule and SpringMethodRule"
date: 2015-08-01 00:10:00 -0500
comments: true
categories: [springframework, spring-test]
---
Spring Framework 4.2.0.RELEASE has arrived and two new rules have been added to spring-framework project `SpringClassRule` and `SpringMethodRule`.

In spring applications we have used `SpringJUnit4ClassRunner` for a long time in our tests but `JUnit` only support one Runner at the time, in order to allow integration between spring with other Runners like `org.junit.runners.Parameterized` we can use these new classes instead of `@RunWith(SpringJUnit4ClassRunner.class)`

* `SpringClassRule` enable the following annotations `@BeforeClass`, `@AfterClass`, `@ProfileValueSourceConfiguration`, `@IfProfileValue`.

* `SpringMethodRule` enable the following annotations `@Before`, `@After`, `@Repeat`, `@Timeout`, `@ProfileValueSourceConfiguration`, `@IfProfileValue`.

Test using classic `SpringJUnit4ClassRunner`.

```java
package io.eddumelendez;

import org.junit.runner.RunWith;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

@RunWith(SpringJUnit4ClassRunner.class)
public class SpringTest {

}
```

Test using new rules `SpringClassRule` and `SpringMethodRule`.

```java
package io.eddumelendez;

import org.junit.ClassRule;
import org.junit.Rule;
import org.springframework.test.context.junit4.rules.SpringClassRule;
import org.springframework.test.context.junit4.rules.SpringMethodRule;

public class SpringTest {

    @ClassRule
    public static final SpringClassRule SPRING_CLASS_RULE = new SpringClassRule();

    @Rule
    public final SpringMethodRule springMethodRule = new SpringMethodRule();

}
```

Both have the same effect in your test and you can use them in different context.
