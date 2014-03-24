---
layout: post
title: "RAML: Designing an API"
date: 2014-09-02 23:28:31 -0500
comments: true
categories: [api, raml, rest]
lang: en
---
As a developers, every day we are working coding many APIs.
But, *what about design?* Sometimes due to the project schedule, too much requirements and even the lack of knowledge about what is `REST`; developers forget about the design of API.  
Months ago I was surfing on the internet, don't remember where but I read:

>`REST`is more than work with `xml` or `json`.

And that's true. So, I researched more about REST and learned lot of things.

## What RAML is?
`RESTful API Modeling Language` allow us to design, describe, define the API. It's human readable and it is visible to everyone.

That's pretty cool, we can design the API and document as well.

## Security
`RAML` supports authentication:

* Basic authentication
* Digest authentication
* Oauth 1.0
* Oauth 2.0

## Book Store API
In the example below, I have designed a Books Store API working my favourite book list.
The API allow me to Create, Read, Update and Delete books. A simple CRUD operation which is represents by HTTP methods.

**OPERATION** | **HTTP METHODS**
--------------|-----------------
CREATE        | POST
READ          | GET
UPDATE        | PUT
DELETE        | DELETE

```
#%RAML 0.8
---
title: Book Store API
version: 1.0
baseUri: http://localhost:8081/api
/books:
  displayName: Books Catalog
  get:
    responses:
      200:
        body:
          application/json:
            example: |
                {
                  "bookId": 1,
                  "title": "Angel & Demons",
                  "isbn": "0-671-02735-2",
                  "authors": [
                    "Dan Brown"
                  ]
                },
                {
                  "bookId": 2,
                  "title": "The Da Vinci Code",
                  "isbn": "0-385-50420-9",
                  "authors": [
                    "Dan Brown"
                  ]
                },
                {
                  "bookId": 3,
                  "title": "The Lost Symbol",
                  "isbn": "978-0-385-50422-5",
                  "authors": [
                    "Dan Brown"
                  ]
                },
                {
                  "bookId": 4,
                  "title": "Inferno",
                  "isbn": "978-0-385-53785-8",
                  "authors": [
                    "Dan Brown"
                  ]
                }
  post:
    body:
      application/json:
        example: |  
            {
             "title": "Deception Point",
             "isbn": "0-671-02738-7",
             "authors": [
              "Dan Brown"
             ]
            }
    responses:
      201:
        description: Book has been successfully created.
      409:
        description: Book already exists.
  /{bookId}:
    displayName: Book
    uriParameters:
      bookId:
        description: |
          Book Identifier
        required: true
    get:
      description: Retrieve book-related information.
      responses:
        200:
          body:
            application/json:
              example:  |
                {
                  "bookId": 1,
                  "title": "Angel & Demons",
                  "isbn": "0-671-02735-2",
                  "authors": [
                    "Dan Brown"
                  ]  
                }
    put:
      description: Update book information.
      body:
         application/json:
          example: |  
            {
             "title": "Inferno",
             "isbn": "978-0-385-53785-8",
             "authors": [
              "Dan Brown"
             ]
            }
      responses:
        204:
          description: |
            The book has been successfully updated.
        404:
          description: |
            Unable to find book with that identifier.
    delete:
      description: Remove book from the catalog.
      responses:
        204:
          description: |
            The book has been successfully removed.
        404:
          description: |
            Unable to find book with that identifier.
```

As you can see, the Book Store API have five services:

* GET http://localhost:8081/api/books
* POST http://localhost:8081/api/books
* GET <http://localhost:8081/api/books/{bookId}>
* PUT <http://localhost:8081/api/books/{bookId}>
* DELETE <http://localhost:8081/api/books/{bookId}>

Learn more about [HTTP Status](http://httpstatus.es/)

## Platforms and Tools
* **Mulesoft** provides an [API Platform](https://anypoint.mulesoft.com/#/signup) and [APIkit](http://www.mulesoft.org/documentation/display/current/APIkit+Tutorial).
* [raml2html](https://github.com/kevinrenskers/raml2html), transform raml file to html.
* [jaxrs-to-raml](https://github.com/mulesoft/jaxrs-to-raml/), generate raml file to existing JAX-RS services. It has been updated today, JAX-RS 2.0 Asynchronous Responses is now supported!!!

There are more RAML projects [here](http://raml.org/projects.html).

## Resources
There are a lot of resources about REST, how to write a good API, some of them are:

* [Roy Thomas Fielding's Dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/fielding_dissertation.pdf)
* [Designing your RESTful API for Longevity](http://blogs.mulesoft.org/designing-restful-api-longevity/)
* [SpringOne2GX 2013 Replay: REST-ful API Design](https://spring.io/blog/2013/12/02/springone2gx-2013-replay-rest-ful-api-design)
* [SpringOne2GX 2013 Replay: REST-Ful API Evolution](http://spring.io/blog/2014/01/14/springone2gx-2013-replay-rest-ful-api-evolution)
* [Rest API Best(?) Practices Reloaded](http://softwaregarden.io/rest-api-best-practices-reloaded/)
