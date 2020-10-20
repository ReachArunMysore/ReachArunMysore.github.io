---
layout: post
title: Notes on Clean Architecture
date: 2020-08-20
category: category
---

* Clean Architecture conforms to The Dependency Rule which says nothing in the inner circle will know anything about the outer circles

* Control Flow
~~~
Outer circle -- to -- Inner circle
web, UI, Device, External Interfaces -> Controller, Gateways, presenter -> Use Case -> Entities
~~~
* Entities are the core of the application. Has the core classes and methods defining the core logic. Nothing in this layer changes if there is any change in the outer layer.
* Use cases are built around entities based on the requirement. Entities and use cases are domain specific.
* Controller, gateways, presenter calls the required use case
* The outermost is the framework, where not much of the code is written.

~~~
Typical application implementation

Entry Point(Controller, gateways, presenters) -> Use Case -> Interface <-- Data Provider(Implements)
~~~

References - 
https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
https://github.com/mattia-battiston/clean-architecture-example
https://pusher.com/tutorials/clean-architecture-introduction
https://github.com/grant-burgess/clean-architecture-example-java-spring-boot