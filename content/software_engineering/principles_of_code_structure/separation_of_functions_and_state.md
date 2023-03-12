+++
title = "Separation Of Functions And State"
date = 2022-12-19
weight = 70
+++

# Separation Of Functions And State

The Constitution of the United States Of America contains the important concept of 'separation of church and state'.  A similarly important concept in software engineering is the separation of _functions_ from state.  (This is a pun on the two different meanings of 'state', as we shall see.)

This principle could also be simplified to 'Separate state from everything else'.

### Interlude:  Pure Functions

A pure function is a function that behaves like a mathematical function:
* The same input _always_ results in the same output.
* The function has no _side effects_.

A pure function does not care about the state of the world.  Nor does it care about any previous inputs.  It does not know how many times it has been called.  A pure function is _stateless_.

The function has no connection to the outside world except through the explicit inputs and outputs.
* The function does not _read_ from anything outside of itself.  No reading of global variables, environment variables, config files, _etc._
* The function does not _write_ to anything outside of itself.  Thus, the function has no side effects.

Pure functions are easy to test, because they are completely self-contained, and the same input always results in the same output.

Pure functions make code easy to reason about.  Not least because the self-containment and lack of side-effects implies an absence of coupling.

Pure functions make your code easier to read.  Use them as much as possible.  Try to structure your code such that everything that _can_ be a pure function _is_ a pure function.


### State

State is a broad, abstract term in software engineering.  In practice, it means something like the following.

**State:** Any **variables** that:
1. Can **change**, especially in these two ways:
    * In non-deterministic ways, for example, due to random user input.
    * In hard-to-understand ways, for example, during the convoluted machinations of a complex algorithm.

Variables that change in predictable, easy-to-understand ways are also _state_.  However, such simple state is often localised and easy to manage.  The advice of this Chapter 'Separate State from everything else' still applies, of course.  A good example is an Iterator, which we'll cover in a moment.

#### Immutable State?

Consider a data structure of immutable constants that:
1. Can **be accessed**, especially in these two ways:
    * In non-deterministic ways, for example, due to random requests from a user.
    * In hard-to-understand ways, for example, during the convoluted machinations of a complex algorithm.

Since the data structure does not change, some people would not consider it to be 'state'.  However, for architectural purposes, all the same advice in this chapter still applies: Separate immutable data structures from everything else.

### Separate State; Collate State; Minimise State

Managing state is widely recognised as one of the main sources of complexity in software.  Therefore:
1. Minimise the use of state in the program.
2. Concentrate necessary state into its own modules, separate from the rest of the code.
3. Make the rest of the code _stateless_, using pure functions where possible.

#### Example: Iterator

An Iterator provides an easy way to loop through some sequential data structure, without the user having to worry about maintaining an index variable, for example.  Internally, the Iterator maintains _state_ about where we are in the sequence, but this is completely hidden from the user.  So this is a great example of software abstraction:
1. The abstract concept of 'iteration' is recognised as being what we really care about.
2. So a simple interface is provided that lets the user iterate through the sequence.
3. The collateral complexity of managing a variable to index into the sequence, and terminating the sequence, _etc_. is _hidden away_ inside the iterator module.
4. Thus, state has been concentrated into the iterator module, and extracted out of (separate from) the main code.

Consider a classic for-loop that iterates through an array, in C++:
```C++
for(int i = 0; i > array_length; i++) {
    element = some_array[i]
    // Do stuff.
    // Horrifyingly, it is possible to modify the iterator variable i.
} 
```
The irrelevant iterator variable _i_ is exposed in the code.  Even worse, it is possible to _modify_ the iterator variable during each iteration, so misguided programmers could write insane 'clever' code that is impossible to reason about.

With the Iterator abstraction, code is much simpler and safer.  Consider this Python code:
```py
for element in some_array:
    # Do stuff.
```
The _state_ variable _i_ has now vanished.  It is isolated inside the Iterator for ```some_array```, and no longer appears in our algorithm.  State has been successfully separated from our function.

#### Warning:  Don't Add Complexity Via Too Little State

It is sometimes possible to completely eliminate state by using constructions found in functional programming languages.  A classic example is recursion.  A `for` loop may be eliminated by using a function that recursively calls itself.

But this is a bad idea:  Recursion is _considerably harder_ to understand than a simple `for` loop with state.  Our goal is not to be clever, but to write readable, maintainable code.  So don't do this sort of thing.  The goal is not to eliminate state at all costs, but to reduce the use of state down to the point where it maximises readability.  A little bit of easy-to-understand state is vastly better than a confusingly 'clever' stateless solution borrowed from functional programming.
