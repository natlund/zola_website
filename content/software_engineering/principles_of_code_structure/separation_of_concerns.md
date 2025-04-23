+++
title = "Separation Of Concerns"
date = 2022-12-19
weight = 50
+++

# Separation Of Concerns

'Concern' is a purposefully broad term. It may refer to:
  * An action, at any level of abstraction
  * A more abstract notion such as 'responsibility' or 'purpose'
  * Data to be stored
  * _Et cetera_.

In some fundamental sense, the process of becoming a good software engineer is the process of learning to discern and define _concerns_ in computer code.  In other words, to get better at abstracting.  To separate concerns, one must first recognise concerns.

The first pillar of good software design is that a module of code that has a single concern is _much easier_ to understand and work with.  So if we find code that deals with more than one concern, we should break it apart into separate pieces that each deal with a single concern.

When designing software from scratch, the abstractions that make up our design should be concerns, and they should already be separated.

When refactoring code, or developing code organically through a series of prototypes, there is an idealised strategy we might follow:
1. Assume we have a prototype piece of code that solves the problem at hand, but is just an unstructured mess.  (Perhaps it is just one long script.)
2. We consider the program as a whole, and ask "What does it do?  What is it for?" and apply our skills of abstraction to answer those questions.
3. We then consider a subset and repeat the same questions.
4. We do this recursively on all parts of the code, figuring what is being done.
5. At length, we will have some idea of all the different _concerns_ in the code.
6. Then we can separate the concerns out, and begin experimenting with a better architecture. 

### Coherence

A piece of code may be described as **coherent** if all of its lines of code relate to a single concern.  A module of code is 'incoherent' if some of its lines of code relate to one concern, and other lines relate to a different concern.

Coherent modules of code are the _consequence_ of correctly separating concerns.

### Collation Of Concerns (Single Concern In A Single Place)

We have established the value of a single module of code only dealing with a single concern.

The complement to that is to pull all the code that deals with the same concern into a single module of code.  In other words, _collate_ all the code that deals a single concern, and put it in a single module.

This concept is important enough to be dealt with fully in its own separate chapter.  (The following chapter [_Single Source Of Truth_](@/software_engineering/principles_of_code_structure/single_source_of_truth.md).)

### Summary: Separate Concerns; Collate Concerns
1. A single module of code should deal with a single concern.
2. A single concern should be dealt with in a single module of code.


A number of concerns have been identified that appear time and time again in many computer programs.  Appropriately separating those particular concerns should be the first order of business when designing a software architecture.  Details follow in the next several chapters.