---
layout: post
lang: en_GB
title:  "Data mocking – Ways to fake a backend (API)"
date:   2016-11-04 00:10:00
category: API
tags: "Data, Mocking, Rest, JSON, API, Frontend, Backend, Fake, Testing"
excerpt: "What are the advantages of working with fake data in projects with a clean seperation between the frontend and the backend?  How can we mock our backend with minimum effort? This blogpost will answer this questions and explains different methods of providing data via a dummy backend."
disqusIdentifier: 2016-06-03-data-mocking-ways-to-fake-a-backend-api
---

Today we mostly have a loose coupling between the frontend and the backend of our web applications. It might be even useful to handle the separate parts as separate projects. Think about the backend as the provider of an RESTful API which has a totally different (hopefully semantic) versioning than the frontend. This offers much more flexibilitylty by being able to deploy only the frontend to production or by using the same backend for a different frontend with a totally different tech stack (eg. native apps).

So in development we have different people working on the frontend and on the backend. The backend team needs to make sure the content the API is providing is sane, whereas the frontend doesn’t care about the content: it just needs dummy data in the correct structure. So these teams only have to talk about and agree on JSON structures before they can work independently on their part.

The main advantage working with dummy data over here is the independence in which the frontend team can work. It doesn't matter if the development of the backend gets stuck for whatever reason.

Which leads us to the question: *How could we simply mock the backend?*

# Different ways to fake a backend

There are a few possibilities to »serve« dummy data depending on your needs, your tech stack and the requirements of your project:

+ Static JSON files via Ajax
+ Online mocking services
+ »JSON Server«
+ An own server

We are going to explore the details as well as the pros and cons of each and every possibility.

## Loading JSON files via Ajax

The simplest approach without any tooling involved. Just create your dummy data and store it within the file system of your frontend project.

### Pros

+ Straightforward
+ The dummy data is in your version control system (eg. Git)

Having those files in your file system has the big advantage, that the dummy data have a single source of truth. This is important for working in the team, especially for the coordination between the frontend and the backend team.

### Cons

+ Very limited functionality
+ Might not be supported by your JavaScript Framework™
+ No usage of HTTP method besides `GET` possible
+ Can’t test handling errors (besides 404)
+ Differences between the fake and the real backend

This might work out for a webapp or website which just loads a little data via Ajax. But other than that the downsides will outweigh the simplicity in most cases. The biggest disadvantages are the differences between your fake backend and the real backend in production. This goes from different URLs (including a whole different structure) to different HTTP headers.

## Online mocking services

There are dedicated services like [mockapi.io](http://www.mockapi.io), [mocky.io](http://www.mocky.io) and [jsonstub.com](https://jsonstub.com/) which offer good solutions to help you effortlessly mock your HTTP responses.

### Pros

+ Easy to use
+ Good and in some cases powerful configuration possibilities

This is almost as easy as storing JSON files in your project. Plus it offers more possibilities to configure things like HTTP status codes and verbs.

### Cons

+ CORS limitations (if applicable)
+ Your own data stored on public servers you don’t own
+ Dependent on vendor
+ Data isn’t in your version control system

The dependency factor is important because it may lead to unforeseeable problems. There is a whole spectrum of uncertainties, mostly related to availability. You should ask yourself at least the following questions: Can I continue working when the service has downtimes? What happens if the service discontinues working? Will it offer any kind of export?

Not having the dummy data under version control is also a major drawback if you are not working alone. Of course you could store the data redundantly in your file system; but that would lead to a maintainability overhead and might cause confusion because no one is sure whether the files in version control are really and exactly mirroring the data served by the mocking service.

## »JSON Server«

[JSON Server](https://github.com/typicode/json-server) is a nifty command line tool and super easy to use even for people who don’t spend most of the day at their terminals.

>Get a full fake REST API with zero coding in less than 30 seconds (seriously)

It boils down to letting you serve JSON from your file system via a local server.

### Pros

+ The dummy data is in your version control system
+ The simplest setup you can imagine
+ It supports the most used http verbs
+ It saves changes to your JSON source for `POST`, `PUT`, `PATCH` or `DELETE` requests.

This sounds like heaven. You can store your fake data in JSON in your project and have an external tool to provide the data.

But there are also a few cons, one or the other of which might be a dealbreaker depending on your project requirements.

### Cons

+ The payload requires a strict format (JSON)
+ No routes with self-defined dynamic parts
  + ~~api/articles/{offset}/{count}~~
+ Maintainability of one single JSON file for your responses

It’s easy to use, however this means some of its conventions could get in your way.

The payload restriction will be no problem if you have full control over the real backend as well. But you will have a problem when your real backend only accepts an integer as payload, to delete a data set for example.

JSON server provides URL parameters for things like pagination. But this is bound to a fixed URL concept you have to adapt. Otherwise you end up having a huge list of URL mappings in a file called [routes.json](https://github.com/typicode/json-server#add-routes). Having this option is advantageous but it may still lack flexibility depending on your needs.

The last possible downside is that putting all your dummy data in one JSON file may not scale well.

## Own server

Writing an own server just to provide your mocked data sounds like a perfect example of overengineering. The question is: Would you – as a frontend developer – maintain something like a »second« backend? Because the main reason to mock your data is to be independent of the backend.

The answer is *yes*, if you can have a reasonable compromise between flexibility and complexity.

[http-fake-backend](https://github.com/micromata/http-fake-backend) offers such compromise. It comes as a Node.js server which serves your dummy data via HTTP. And it’s almost as easy to set up as »JSON server«. It basically lets you build a fake backend by providing the content of JSON files or JavaScript objects through configurable routes.

Each endpoint needs a configuration file to define routes, HTTP method and the response.

### Simple example

Let’s say you need an endpoint like `http://localhost:8081/api/simpleExample` which should return:

```javascript
{
  "status": "ok"
}
```

All you have to do is create a configuration in a JavaScript file like:

```javascript
module.exports = SetupEndpoint({
    name: 'simpleExample',
    urls: [{
        requests: [{
          response: {status: 'ok'}
        }]
    }]
});
```

### Advanced example

But it’s way more flexible than responding JSON defined through a JavaScript object via HTTP `GET`.

Let’s look at a more complex example configuration like the following:

```javascript
module.exports = SetupEndpoint({
    name: 'anotherExample',
    urls: [{
        params: '/read',
        requests: [{
            method: 'GET',
            response: '/json-templates/anotherExample.json'
        }]
    }, {
        params: '/update/{id}',
        requests: [{
            method: ['PUT', 'PATCH'],
            response: {
                success: true
            }
        }, {
            method: 'DELETE',
            response: {
                deleted: true
            }
        }]
    }]
});
```

So you can have multiple urls with different HTTP verbs for any endpoint and you can define your Response via JSON files.

You can also fake HTTP errors and status codes for an entire endpoint or on request level like in the following example:

```javascript
module.exports = SetupEndpoint({
    name: 'statusCodes',
    urls: [
        {
            params: '/boomError',
            requests: [{
                // Returns a 402 status code + error message provided by boom:
                // {
                //   "error" : "Payment Required",
                //   "statusCode" : 402
                // }
                statusCode: 402
            }]
        },
        {
            params: '/customError',
            requests: [{
                // Returns a HTTP status code 406 and a self defined response:
                response: { error: true },
                statusCode: 406
            }]
        },
        {
            params: '/regularResponse',
            requests: [{
                // Returns a 401 error provided by boom
                // as defined on endpoint level
                response: '/json-templates/anotherExample.json'
            }]
        }
    ],
    statusCode: 401
});
```

The configuration object described in detail:

* `name`  
  * Is used to set the endpoint.
* `urls`
  * You need to add at least one url object.
* `urls.params`
  * Optional
  * In this example a valid URL might be:
    `http://localhost:8081/api/articles/foo/bar/baz`
    whereas:
    `http://localhost:8081/api/articles` will return a 404 error.
  * See hapi docs. For example regarding optional [path parameters](http://hapijs.com/api#path-parameters).
* `urls.requests`
    *  You need to add at least one request object.
* `urls.requests.method`
    * optional. Uses `GET` when not defined.
    * `string`, or `array` of strings.
    * is used to define the http method(s) to which the endpoint will listen.
* `urls.requests.response`
  * Could be a string pointing to a JSON template:
    *   `response: '/json-templates/articles.json'`
  * Or just a JavaScript object:
    * `response: { success: true }`
* `urls.requests.statusCode`
  * Optional
  * A status code (number)
  * Will return:
    * a status code with a self defined response if you provide a response property
    * a status code with a predefined error object provided by [boom](https://github.com/hapijs/boom) if you dont provide a response property for that request.
* `statusCode`
  * Optional
  * Every route of this endpoint will return a HTTP error with the given status code provided by [boom](https://github.com/hapijs/boom).

People who think that this looks daunting can create a config like this easily and interactively with the help of this [Yeoman generator](https://github.com/micromata/generator-http-fake-backend) which comes with a subgenerator which guides through the configuration:

![yeoman](https://d17oy1vhnax1f7.cloudfront.net/items/170V1V1a3H1q1C0g3d3y/demo.gif)

### It offers even more flexibility

Just when you need it: You can build own endpoints with custom configs since the server underneath is just a simple http server built with [hapi](http://hapijs.com/).

### Pros

+ The dummy data is in your version control system
+ The highest flexibility
+ Easy setup of
  + Endpoints
  + URLs including dynamic parts
  + allowed HTTP methods
  + errors (supporting all HTTP status codes)
+ Yeoman generator
  + with a subgenerator to assist with building the API

It also optionally restarts the server when JSON or config files are changed. Just like JSON server.

### Cons

+ Slightly more complex setup compared to JSON server
+ Less intelligent than JSON server
  + No persisting of payload data for POST, PUT and PATCH requests
  + No automatic and real relation between data of different endpoints
    + Example:
        + You have to define own and independent data for a route which returns a list `/api/products` and a route which returns a single item `/api/products/{id}`

### Workflow integration

Starting the server is as easy as firing `npm run start:dev` during development or `npm start` in a Continous Integration environment. No matter if you are using npm run scripts or a workflow based on a taskrunner to build your frontend.

### Getting started

Just visit the projects [Github page](https://github.com/micromata/http-fake-backend) and you will have your fake backend running in a couple of minutes. You are even faster when using the [Yeoman Generator](https://github.com/micromata/generator-http-fake-backend).

## Helpers for generating your dummy data

Developers aren’t lazy per se. But we all like to dispense with stupid and repetitive work. So we could need some help generating the content for our fake backend. This is where the following tools might come in handy.

### JSON generators

The following tools could help you to generate JSON files for fake backend:

+ https://github.com/danibram/mocker-data-generator/
+ http://www.json-generator.com/

### Dummy data generators

Feel free to use one of these excellent node modules if you prefer to build the responses of your fake backend programmatically:

+ https://github.com/Marak/faker.js
+ https://github.com/boo1ean/casual
+ https://github.com/chancejs/chancejs/
