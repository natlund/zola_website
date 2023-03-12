+++
title = "Separate Business Logic From Mechanical Work"
date = 2022-12-19
weight = 100
+++

# Separate Business Logic From Mechanical Work

Business logic is the _whole point_ of software.  Software is engineered to solve business problems.

Therefore, in your code, _highlight_ the business logic.  Try to elevate it to its own module so that the business logic is _obvious_.  This also tends to make it easier to modify the business logic.

Code is often read for debugging purposes, or to answer a question about system behaviour that is not documented.  These are issues of business logic: "What is the system supposed to do, and is it actually doing it?"  Therefore, make life easy for everybody by making business logic extremely explicit, sitting by itself in an easy-to-find place.  Keep it _separate_ from low-level mechanical details about _how_ the system implements that business logic.

Deciding what counts as business logic may not always be easy.  But try to keep this separation in mind when designing the system.  This abstraction is one that _matters_.
