+++
title = "Readable Code Structure"
date = 2022-03-14
weight = 1
draft = true
+++

_High-level notes on good computer code structure, made early in 2022.  We list individual topics, some of which could be a 'Chapter' in their own right. For each topic, notes are made.  Some chapter notes are nearly complete; others are only sketches._

_Shortly after writing the first draft, I formulated an important concept: the separation of function and state.  That principle clarifies a lot of things, including when to use objects.  Since this document was written before realising the central importance of state, this document will probably be adandoned and cannibalised to provide material for new, better essay._

## "What the hell does this do?"

Readability is the only thing that matters.  In rare circumstances, speed may be important enough to override readability concerns.

Readability: The inverse time taken to understand a piece of code.  The inverse time taken to satisfactorily answer the question "What does this code do?"


## A Couple of Structures

Linear: List like.  A linear sequence of objects or actions.

Tree: Self-explanatory.  Best explained with a diagram.


## A Couple of Kinds of Code

Algorithm-like: A sequence of actions to be performed in order.  There may be conditional branching.
Often follows the pattern handed down from the ancients:
    - Get some input data.
    - Derive things from the input data.  Transform the input data into output data.
    - Put the output data somewhere.  Return the output data.


Data-like: Static. Code that represents input or output data, state, configuration, etc.


## Principle:  Separation Of Concerns.  Single Responsibility Principle.

Even grumpy old Uncle Bob gets this right.

Code is much more readable if each separate piece of code only does one thing.

Very Important Corollary:  Do not mix algorithm-like and data-like code.
We'll come back to this.


## Principle:  Code Should Look Like What It Is.  Code Should Look Like What It Does.

Algorithm-like code should be structured in a linear fashion.

Very simple data-like code can be flat (linear).  But more complex Data-like code can benefit from a tree structure.  Consider a humungous, flat JSON blob, versus a sensibly grouped and nested tree hierarchy of the same data.


## The Fundamental Cause Of Badly-Structured Code

Why do intelligent people write such obfuscated, tangled code?  Here is why:

They are organising code as if it nothing more than a static bunch of text statements.  Of course, it *is* a static bunch text statements, but crucially, it may be *more* than that: there is another dimension to consider.  We'll come back to this point.

The intelligent but unwise programmer looks at code as a bunch of static text statements, and proceeds to 'organise' it.  The programmer abstracts out an underlying logical structure, and breaks the code into separate parts.  He or she carries on, further breaking each newly-created part into separate logical chunks.  The final result is a large number of separate pieces, all connected together in a **tree** structure.  The intelligent but unwise programmer is probably proud of this achievement, believing that he or she has cleverly followed the Separation Of Concerns Principle to the letter.  The code is now so beautifully *organised*.

Now, this is fine as long as the code is **Data-like**.

But most code in an application is algorithm-like. For algorithm-like code, this approach is completely and utterly wrong.  As we noted above, there is another dimension: time.  More specifically: execution order.

Algorithm-like code consists of a series of actions performed in a sequence.  To understand the code, one must understand the exact sequence of actions.  A linear structure obviously perfectly captures the sequence of actions.  On the other hand, a tree structure *obfuscates* the sequence of actions.

This is important enough to get its own chapter.


## The Fundamental Skill Of Software Engineering.

Separating code into algorithm-like and data-like components, and coding each component appropriately.

Algorithm-like code should follow these principles:
    1. Principle Of Obvious Execution Flow.
    2. Principle Of Explicit Dependencies.
    3. Principle That Data Flow Should Match Execution Flow.
    4. Concluding Principle That The Object-Oriented Paradigm Sucks For Algorithm-like Code.

Data-like code tends to be simpler.  Principles 1. to 3. for algorithm-like code also apply, to the extent that they are relevant.  The big difference is this principle:
    - Concluding Principle That The Object-Oriented Paradigm Is A Good Match For Data-like Code.

## Principle Of Obvious Execution Flow

If code *has* an execution flow, i.e. it is algorithm-like, then that execution flow is the most important thing.  The execution flow **is** the algorithm.  Therefore, the code should make that execution flow as obvious as possible.

A linear structure makes the execution flow as explicit as possible.  A tree-like structure conceals the execution flow.


## Principle of Explicit Dependencies.

The question "What does this code do?" implicitly includes the sub-question "What does this code depend on?"

Dependencies include:
    - imports
    - input data
    - config read from a file
    - config read from an Operating System environment variable.
    
Simple Rule: Put all dependencies explicitly at the start of the algorithm.


## Principle That Data Flow Should Follow Execution Flow

Global variables are evil.  Everyone knows that.  But if you re-label them as 'class variables', then suddenly everone thinks they are wonderful.


## OOP Classes Suck for Algorithm-like Code



## When To Use Object-Oriented Code.

The traditional (and still the best) use case for Objects is this:
    - Objects are for carrying around **state** that can be randomly accessed.
    
This includes:
    - State that can be mutated or accessed at random times or places in the app.
    - State that is complex data, that needs non-trivial algorithms to access the data, transform it, and present it in a convenient format.
    - State comprised of variables that have a specific relationship to each other.  The relationship can be enforced by a 'setter' method or factory method that validates the input data and/or derives some variables from others.
