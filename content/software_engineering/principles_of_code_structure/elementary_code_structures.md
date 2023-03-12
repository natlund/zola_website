+++
title = "Elementary Code Structures"
date = 2022-12-19
weight = 20
+++


This _Principles Of Code Structure_ is not intended for complete beginner programmers.  Nevertheless, to prevent any possible confusion, we shall describe the two most common structural elements found in most modern computer languages.

### Functions
In earlier languages, they were also known as 'subroutines' or 'procedures'.  While subtle distinctions may be claimed between subroutines, procedures, and functions, modern usage has seemed to settle on a conception of function that is allied as closely as possible with the mathematical definition of a function.

A **function** in a programming language is a self-contained piece of code, that optionally takes some inputs, does some actions, and optionally returns an output.

### Objects
While the original conceptions of objects came out of Object-Oriented Programming, structures equivalent to objects are now available in most professional languages.  (For example, the functional programming language Clojure has 'Records' which work like objects.)

An **object** in a programming language is a single 'container' data structure, that may hold many different kinds of data, and may also have functions that are attached in some way to that data structure.  The key feature is that the functions - typically called 'methods' - can be accessed _via the data structure_ in the syntax of the language.
