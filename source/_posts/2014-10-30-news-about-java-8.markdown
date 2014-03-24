---
layout: post
title: "News about Java 8"
date: 2014-10-30 22:09:19 -0500
comments: true
categories: [java, java 8, lambdas, streams]
lang: en
---
Java 8 was released in March and many cool features have arrived in a functional programming style.

## Lambdas

Lambdas has been used in other programming languages. In `java`, it's the new way to call `anonymous classes`.

If you have been Swing developer, you may have seen lot of this code. Example of `anonymous class`:

```java
File[] directories = new File(System.getProperty("user.home")).listFiles(new FileFilter() {
           @Override
           public boolean accept(File pathname) {
               return pathname.isDirectory();
           }
       });
```

Below, you can see three approaches to use lambdas:

```java
() -> System.out.println("Hello lamdba");

//pass an object
customer -> customer.getLastname();

//using blocks
() -> {
  String greeting = "Hello lambda block";
  System.out.println(greeting);
}
```

Now, let write our first example using lambdas:

```java
File[] directories = new File(System.getProperty("user.home"))
                .listFiles((File pathname) -> pathname.isDirectory());
```

In this example, to move from `anonymous class` to `lambdas` there are two steps to do. As you can see the difference is inside of `listFiles` method. The first part of the lambda is the parameter of the method `accept` (File pathname) next the arrow (->) and finally the return statement (pathname.isDirectory()). If you want to add extra functionality inside of the lambda you can use block statements.

## Streams API

The power to manage collections with readable code is here.

I will work in this example with my favourite books. So, we will print in the console only books that contains *"o"*

Old fashionable way:

```java
List<Book> books = new ArrayList<>();
books.add(BookBuilder.defaultValues().withId(1l).withTitle("Angel & Demons").withIsbn("0-671-02735-2").build());

books.add(BookBuilder.defaultValues().withId(2l).withTitle("The Da Vinci Code").withIsbn("0-385-50420-9").build());

books.add(BookBuilder.defaultValues().withId(3l).withTitle("The Lost Symbol").withIsbn("978-0-385-50422-5").build());

books.add(BookBuilder.defaultValues().withId(4l).withTitle("Inferno").withIsbn("978-0-385-53785-8").build());

for(Book book : books){
  if (book.getTitle().contains("o")) {
    System.out.println(book.getTitle());
  }
}
```

Now we will use Stream API to rewrite the last part:

```java
List<String> bookNames = books.stream()
.filter(book -> book.getTitle().contains("o"))
.map(Book::getTitle).collect(Collectors.toList());
System.out.println(bookNames);
```

Both are doing the same thing but stream offers another great cool features like parallelStream or group function. Additionally, it is readable code and the `ciclomatic complexity` is reduced.

There are `eager` and `lazy` methods inside of Streams API.

- Eager, return some value or void. Ex: foreach, collect.
- Lazy, return another stream. Ex: filter, map.

**Note:** Streams can be read just once. If you try to work with the same stream twice you will se an exception.

For more infomation about Streams visit the [official documentation](http://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html).

## Default Methods

In java 8, there are big changes like this. Do you remember interfaces? The place where you define what to do and the class implementation define how.

Default methods has been used in the Java 8 API in order to add new functionality without break existing code. Take a look inside `Collection.java` you will se that `stream()` method is a default method.

If you have take a look inside of the API you can see that default method has body or define an action.

```java
public interface Greeting {

  public default void welcome() {
    System.out.println("Hi, I am a default method.")
  }

}

class SpanishGreeting implements Greeting {

  @Override
  public void welcome() {
    System.out.println("Hola, soy un método por defecto.")
  }

}

class EnglishGreeting implements Greeting {

}
```

If we call welcome method from SpanishGreeting "Hola, soy un método por defecto." will be printed but if you call the method from EnglishGreeting "Hi, I am a default method." will be printed.


## Method References

Everything can be well used or not, in the case of lambdas does nothing, just call the method you can use method references as a easy-to-read approach.

```java
Customer::getFirstname //instead  customer -> customer.getFirstname()
```
