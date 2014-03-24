---
layout: post
title: "JUnit and Mockito"
date: 2014-03-23 20:55:45 -0500
comments: true
categories: [junit, mockito, maven]
lang: en
---
As you maybe know, [JUnit](http://junit.org/) is a java testing framework.

Before to talk about our mock framework, we need to be in the same page about what mock is?

Marting Fowler in his article [Mocks are not Stubs](http://martinfowler.com/articles/mocksArentStubs.html) said:
> Mocks are objects pre-programmed with expectations which form a specification of the calls they are expected to receive.

[Mockito](https://code.google.com/p/mockito/) is the mock framework which we will use.

Lets start with the example, first of all we need to setup our Maven project.

**1.** Adding dependencies

{% codeblock lang:xml+evoque pom.xml%}
<dependencies>
	<dependency>
		<groupId>junit</groupId>
		<artifactId>junit</artifactId>
		<version>4.10</version>
		<scope>test</scope>
	</dependency>
	<dependency>
		<groupId>org.mockito</groupId>
		<artifactId>mockito-all</artifactId>
		<version>1.8.5</version>
		<scope>test</scope>
	</dependency>
</dependencies>
{% endcodeblock %}

**2.** In this example, we will use annotations so we have three ways to enable them.

{% codeblock lang:java UserServiceImplTest.java%}
@RunWith(MockitoJUnitRunner.class)				//First method to enable mockito's annotations
public class UserServiceImplTest {

	@Rule
	public MockitoRule rule = MockitoJUnit.rule();	//Second method to enable mockito's annotations

	@Before
	public void setup() {
		MockitoAnnotations.initMocks(this);		//Third method to enable mockito's annotations
	}

}
{% endcodeblock %}

**Note: You can use one of them. I suggest the use of `MockitoRule` in favor of use another runners like `org.junit.runners.Parameterized`**

**3.** UserServiceImpl HAS-A UserRepository. For that reason, create a UserRepository mock and it will be injected in UserServiceImpl. Then, we can mock UserRepository methods as you can see in step 3.

{% codeblock lang:java UserServiceImplTest.java%}
public class UserServiceImplTest {

	@Mock								//1. Create UserRepository mock object
	UserRepository userRepository;

	@InjectMocks						//2. Insert UserRepository mock object into UserService
	UserService userService = new UserServiceImpl();

	@Before
	public void setup() {
		//MockitoAnnotations.initMocks(this);
	}

	@Test
	public void testSomething() {
		String username = "emelendez";
		Mockito.when(userRepository.getPassword(username)).thenReturn("PasswordMock"); //3. Mocking objects
		userService.validateCredential(username);
		Mockito.verify(userRepository).getPassword(username);
	}

}
{% endcodeblock %}

You can download the source code [here](https://github.com/eddumelendez/mockito)
