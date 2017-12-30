# JAX-RS - Java API for RESTful Web Services

* [Wikipedia - Representational State Trasnfer](https://en.wikipedia.org/wiki/Representational_state_transfer)

## Introduction

Java's implementation of REST (Representational State Transfer), which simplifies the creation of the RESTful API. Originally standardised in EE 6, and then improved in EE 7 and EE 8.

* JAX-RS is version 2.1 as of Java EE 8
* Supports [hypermedia](https://en.wikipedia.org/wiki/Hypermedia) by following [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS) model
* HATEOS: Hypermedia As The Engine of Application State - this allows for dynamically navigating the REST API via context relevant links (a response to a request may contain additional contextually relevant links)
* URL + HTTP verb + HTTP body = REST
* Used to represent and tansfer resources, which could be XML, HTML, JSON, etc. Often with JAX-RS the resource is a serialised POJO represented as a JSON string.
* Similar to CRUD (map CRUD to equivalent HTTP verbs): Create -> Post, Read -> GET, Update -> PUT, Delete -> DELETE
* Provides a server and client API
  * Client API is a higher level abstraction than HttpURLConnection