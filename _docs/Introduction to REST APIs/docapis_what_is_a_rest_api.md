---
title: What is a REST API?
permalink: /docapis_what-is-a-rest-api.html
keywords:
course: "Documenting REST APIs"
weight: 1.2
sidebar: docapis
section: introtoapis
---


## An API is an interface between systems

{% include note.html content="This course is all about learning by doing, but while <i>doing</i> various activities, I'll periodically pause and dive into some more abstract concepts to fill in more detail. This is one of those deep dive moments." %}

In general, an API (or Application Programming Interface) provides an interface between two systems. It's like a cog that allows two systems to interact with each other.

<a href="http://bit.ly/1DexWM0"><img src="images/spinning_gears.jpg" alt="Spinning gears. By Brent 2.0. Flickr." /></a>

In an API workshop by Jim Bisso, an experienced API technical writer in the Silicon Valley area, Bisso said to consider your computer's calculator. When you press buttons, functions underneath are interacting with other components to get information. Once the information is returned, the calculator presents the data back to the GUI.

<img src="images/calculator.png" alt="calculator" />

APIs often work in similar ways. But instead of interacting within the same system, web APIs call remote services to get their information.

Developers use API calls behind the scenes to pull information into their apps. A button on a GUI may be internally wired to make calls to an external service. For example, the embedded Twitter or Facebook buttons that interact with social networks, or embedded Youtube videos that pull a video in from youtube.com, are both powered by web APIs underneath.

## APIs that use HTTP protocol are "web services"

In general, a web service is a web-based application that provides information in a format consumable by other computers. Web services include various types of APIs, including both REST and SOAP APIs. Web services are basically request and response interactions between clients and servers (a computer makes the request, and the web service provides the response).

All APIs that use HTTP protocol as the transport format for requests and responses can be classified as "web services."

## Language agnostic

With web services, the client making the request and the API server providing the response can use any programming language or platform &mdash; it doesn't matter because the message request and response are made through a common HTTP web protocol.

This is part of the beauty of web services: they are language agnostic and therefore interoperable across different platforms and systems.

## SOAP APIs are the predecessor to REST APIs

Before REST became the most popular web service, SOAP (Simple Object Access Protocol) was much more common. To understand REST a little better, it helps to have some context with SOAP. This way you can see what makes REST different.

### SOAP used standardized protocols and WSDL files

SOAP is a standardized protocol that requires XML as the message format for requests and responses. As a standardized protocol, the message format is usually defined through something called a WSDL file (Web Services Description Language).

The WSDL file defines the allowed elements and attributes in the message exchanges. The WSDL file is machine readable and used by the servers interacting with each other to facilitate the communication.

SOAP messages are enclosed in an "envelope" that includes a header and body, using a specific XML schema and namespace. For an example of a SOAP request and response format, see [SOAP vs REST Challenges](http://www.soapui.org/testing-dojo/world-of-api-testing/soap-vs--rest-challenges.html).

### Problems with SOAP and XML: Too heavy, slow

The main problem with SOAP is that the XML message format is too verbose and heavy. It is particularly problematic with mobile scenarios where file size and bandwidth are critical. The verbose message format slows processing times, which makes SOAP interactions more slow.

SOAP is still used in enterprise application scenarios with server-to-server communication, but in the past 5 years, SOAP has largely been replaced by REST, especially for APIs on the open web. You can browse some SOAP APIs at [http://xmethods.com/ve2/index.po](http://xmethods.com/ve2/index.po).

## REST is a style, not a standard

Like SOAP, REST (REpresentational State Transfer) uses HTTP as the transport protocol for the message requests and responses. However, unlike SOAP, REST is an architectural style, not a standard protocol. This is why REST APIs are sometimes called _RESTful_ APIs &mdash; REST is a general style that the API follows.

A RESTful API might not follow all of the official characteristics of REST as outlined by [Dr. Roy Fielding](https://en.wikipedia.org/wiki/Roy_Fielding), who first described the model. Hence these APIs are "RESTful" or "REST-like."

## Requests and Responses

Here's the general model of a REST API:

<img src="images/restapi_restapi.png alt="REST API" />

As you can see, there's a request and a response between a client to the API server. The client and server can be based in any language, but HTTP is the protocol used to transport the message. This request-and-response pattern is fundamentally how REST APIs work.

### Any message format can be used with REST

As an architectural style, you aren't limited to XML as the message format. REST APIs can use any message format the API developers want to use, including XML, JSON, Atom, RSS, CSV, HTML, and more.

### JSON most common format

Despite the variety of message format options, most REST APIs use JSON (JavaScript Object Notation) as the default message format. This is because JSON provides a lightweight, simple, and more flexible message format that increases the speed of communication.

The lightweight nature of JSON also allows for mobile processing scenarios and is easy to parse on the web using JavaScript. In contrast, with XML you have to use XSLT to parse and process the content.

### REST focuses on resources accessed through URLs

Another unique aspect of REST is that REST APIs focus on *resources* (that is, *things*, rather than actions, which is what SOAP does), and ways to access the resources. You access the resources through URLs (Uniform Resource Locations). The URLs are accompanied by a method that specifies how you want to interact with the resource.

Common methods include GET (read), POST (create), PUT (update), and DELETE (remove). The URL usually includes query parameters that specify more details about the representation of the resource you want to see. For example, you might specify (in a query parameter) that you want to limit the display of 5 instances of the resource.

{{tip}}The relationship between resources and methods is often described in terms of "nouns" and "verbs." The resource is the noun, because it is an object or thing. The verb is what you're doing with that noun. Combining nouns with verbs is how you form the language in REST." %}

### Sample URLs for a REST API

Here's what a sample REST URI or endpoint might look like:

```
http://apiserver.com/homes?limit=5&format=json
```

This endpoint would get the "homes" resource and limit the result to 5 homes. It would return the response in JSON format.

You can have multiple endpoints that refer to the same resource. Here's one variation:

```
http://apiserver.com/homes/1234
```

This might be an endpoint that retrieves a home resource with an ID of `1234`. What is transferred back from the server to the client is the "representation" of the resource. The resource may have many different representations (showing all homes, homes that match a certain criteria, homes in a specific format, and so on), but here we want to see home 1234.

### The web itself follows REST

The terminology of "URIs" and "GET requests" and "message responses" transported over "HTTP protocol" might seem unfamiliar, but really this is just the official REST terminology to describe what's happening. If you've used the web, you're already familiar with how REST APIs work, because the web itself essentially follows a RESTful style.

If you open a browser and go to http://idratherbewriting.com, you're really using HTTP protocol (`http://`) to submit a GET request to the resource available on a web server. The response from the server sends the content at this resource back to you using HTTP. Your browser is just a client that makes the message response look pretty.

{% unless site.target == "pdf" %}
<img src="images/restapi_www.svg" alt="Web as REST API" />
{% endunless %}

{% if site.target == "pdf" %}
<img src="images/restapi_www.png" alt="Web as REST API" />
{% endif %}

You can see this response in cURL if you open a Terminal prompt and type `curl http://idratherbewriting.com`.

Because the web itself is an example of RESTful style architecture, the way REST APIs work will likely become second nature to you.

### REST APIs are stateless and cacheable

Some additional features of REST APIs are that they are stateless and cacheable. Stateless means that each time you access a resource through an endpoint, the API provides the same response. It doesn't remember your last request and take that into account when providing the new response. In other words, there aren't any previously remembered states that the API takes into account with each request.

The responses can also be cached in order to increase the performance. If the browser's cache already contains the information asked for in the request, the browser can simply return the information from the cache instead of getting the resource from the server again.

Caching with REST APIs is similar to caching on web pages. The browser uses the last-modified-time value in the HTTP headers to determine if it needs to get the resource again. If the content hasn't been modified since the last time it was retrieved, the cached copy can be used instead. This increases the speed of the response.

REST APIs have other characteristics, which you can dive more deeply into on [REST API Tutorial](http://www.restapitutorial.com/lessons/whatisrest.html). One of these characteristics includes links in the responses to allow users to page through to additional items. This feature is called HATEOAS, or Hypermedia As The Engine of Application State.

Understanding REST at a higher, more theoretical level isn't my goal here, nor is this knowledge necessary to document a REST API. However, there are a number of more technical books, courses, and websites that explore REST API concepts, constraints, and architecture in more depth that you can consult to dive deeper here. For example, check out *Foundations of Programming: Web Services* by David Gassner on lynda.com.

### REST APIs don't use WSDL files, but some specs exist

An important aspect of REST APIs, especially in terms of documentation, is that they don't use a WSDL file to describe the elements and parameters allowed in the requests and responses.

Although there is a possible WADL (Web Application Description Language) file that can be used to describe REST APIs, they're rarely used since the WADL files don't adequately describe all the resources, parameters, message formats, and other attributes the REST API. (Remember that the REST API is an architectural style, not a standardized protocol.)

In order to understand how to interact with a REST API, you have to *read the documentation* for the API. (Hooray! This makes the technical writers' role extremely important with REST APIs. )

Some formal specifications &mdash; for example, Swagger (also called OpenAPI) and RAML &mdash; have been developed to describe REST APIs. When you describe your API using the Swagger or RAML specification, tools that can read those specifications (like Swagger UI or the RAML API Console) will generate an interactive documentation output.

The Swagger or RAML output can take the place of the WSDL file that was more common with SOAP. These spec-driven outputs are usually interactive (featuring API Consoles or API Explorers) and allow you to try out REST calls and see responses directly in the documentation.

But don't expect Swagger UI or RAML API Console documentation outputs to include all the details users would need to work with your API (for example, how to include authorization keys, details about workflows and interdependencies between endpoints, and so on). The Swagger or RAML output usually contains reference documentation only, which typically only accounts for part of the total needed documentation.

Overall, REST APIs are more varied and flexible than SOAP, and you almost always need to read the documentation in order to understand how to interact with a REST API. As you explore REST APIs, you will find that they differ greatly from one to another (especially the format and display of their documentation sites), but they all share the common patterns outlined here. At the core of any REST API is a request and response.
