---
layout: post
title: Developing RESTful APIs using Node.js, Typescript, and Postgres - Part 1
categories: tutorials,node.js,typescript,postgres
date: 2017-01-06
tags: tutorials,node.js,typescript,postgres
---

One of the best use cases for Node.js is for usage in nonblocking i/o. This behavior can be used to our advantage when developing RESTful APIs using Node.js. Javascript is notorious as a language. Writing maintainable code using javascript is tough. To make our code readable and maintainable, we will be using typescript.

While there are a lot of libraries to create an HTTP Server

To make it testable, we will be using the dependency injection library known as InversifyJS. 

VS Code will be our text editor.

We'll store our data in PostgreSQL using an excellent pg-promise library.

We'll  unit test our controllers and services using Jest and use SuperTest for integration tests.

In the end, we'll learn how to deploy our REST API with NGINX for reverse proxy and Docker for container orchestration.