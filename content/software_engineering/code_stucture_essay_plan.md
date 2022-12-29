+++
title = "Code Structure - Essay Plan"
date = 2022-01-02
weight = 1
draft = true
+++

Options for a plan for the main essay/book on Code Structure.  Each plan is a logical structure for the arguments.  Obviously, there may be more than one optimum logical structure.

My understanding of code structure grew a hell of a lot over 2022, and I have tried to capture the essay structure I considered best at various points in time.

## Option 1  Early 2022

1. Intro - readability, tree vs linear.
2. State Axiom: Separation of Functions and State
3. Principles of Readability.
   - Code should look like what it is.  Code should look like what it does.
      - Separation of concerns
   - Obvious execution flow
   - Data Flow follows Code flow.
   - Explicit dependencies
4. Advice to use Objects for State only.
5. How typical OO violates principle of readability
6. Fundamental cause of bad code (tree structure for linear algorithm)
7. A common mal-abstraction: assembling all required ingredients into an 'abstraction'.

State Axiom: Separation of Functions and State.

Need to think how the five principles interact with the state axiom.  Is the state axiom just another principle?  No, I think it is foundational. Should those principles be introduced before the advice to ruthlessly minimise state?  Or are those principles really just ways to explain what goes wrong if state is splattered everywhere, eg. why OO almost always sucks?


Uncle Bob's 'Separation Of Concerns' would still violate my other principles.  Eg. Uncle Bob would happily bundle a single 'concern' into an object that maintains state _as well as_ containing functions (methods).  This may or may not be appropriate.  What _is_ appropriate is to _ruthlessly_ minimise state.


## Option 2 September 2022,

In the last six months, my (erstwhile) manager at Yobota, Guy Billings, sent me _Modern Software Engineering_ by Dave Farley.  I read that, and discussed elements of it with him.  Unfortunately, he quit before I could fully explore all the things I wanted to with him.

That book contains very good principles, though the ideas have obvious extensions that he fails to see, and the book is quite poorly written.  Reading that book gave me a couple of epiphanies, based on integrating and extending the ideas that Dave Farley presents.  So my conception of optimum code structure has grown and improved substantially in the last six months.

New Ideas:

The big one:  Separate Concerns is the Golden Rule, the Prime Directive.

Defining what a 'Concern' is, is the key task of building a theory of code structure.

Concerns to separate:

1. Functions from State.
2. Coupling is a Key Concern.  Putting the coupling in as few places as possible.  Wait, maybe this rule should be elevated to stand alongside Separation Of Concerns.

So maybe:
* Separate Concerns.
  * Separate Functions From State.
  * Separate Inherent Complexity from Collateral Complexity.  (And eliminate unnecessary Accidental Complexity.)
* Coupling Is Key.  Coupling is King.  Coupling is a Key Concern.



## Option 3 December 2022

1. Readability is the only metric that matters.  (Except very occasionally, speed.)
1. Elementary code structures:  Functions and Objects.  Just enough to introduce them, and define them well enough so that we can agree that even functional languages like Clojure effectively have objects.
2. At the highest level, a couple of kinds of code: Algorithm-like and Data-like.  **Maybe this chapter should come before introducing functions and objects?**
3. A couple of abstract structures: Linear and Tree.

4. Properties of Readable Code?  Hmm.  Most of the below belongs in the _Coupling_ section below, I think.
    * It looks like what it _is_.  It looks like what it _does_.  Linear structure for Algorithm-like; Tree structure for Data-like.
    * Obvious Execution Flow.
    * Data Flow Follows Execution Flow.
    * Obvious Dependencies
    * The main cause of bad code:  Nerds 'organise' algorithm-like code into nested, hierarchical tree structures.

    Perhaps we should come back to this again as an epilogue: "Properties Of Readable Code Revisited".

5. Interlude:  The Art of Abstraction.
   * Malabstraction.  Peasant Abstraction: bundling all the ingredients required into one component and calling it an 'abstraction'.
    * Need to mention the evil of Abstraction Addiction, making things as abstract as possible.  Probably should go in a separate chapter, perhaps even after the core bit on separation of concerns and clarity of coupling.

6. The Twin Pillars:  Separation Of Concerns and Clarity Of Coupling.  Once Concerns have been separated, how are they connected?  The separated concerns and the coupling between them are two sides of the same coin.  They define the totality of your software architecture.  Deciding on what the concerns are and how they connect is what software architecture _is_.

7. Separation of Concerns.  Figuring out what the concerns are is the essence of good engineering.  The skill of abstraction is what allows engineers to do this well.  It is not trivial, and cannot be done by mindlessly following some rules.  However, we can start with the following things, that almost always should be separated.
    * Inherent Complexity and Collateral Complexity.
    * Functions and State
    * Functions and Output. Code that builds things, and code that represents the things built.  'Verb' code from 'Noun' code.  Algorithm-like code from data-like code.
    * IO from Computation
    * Business Logic from mechanical computation.
    

    Furthermore, the inverse of separation of concerns also applies: Collection of Single Concerns/Centralise Concerns.
    * A single piece of code should deal with one concern.
    * A single concern should be handled in one piece of code.

8. Complexity in software.  Three types: inherent, collateral, accidental.  Separate inherent complexity from collateral complexity.  Eliminate accidental complexity.  (This separation is easy for beginners to understand.  It is where the novice first begins to think like an engineer.)

9.  Separation Of Functions And State.  Analagous to the USA's separation of church and state.
    * Interlude:  Pure functions.  Use these as much as possible.
    * Interlude:  Immutability.  Use immutable data structures as much as possible.
    * Definition:  State.  Variables that need to be mutated in ways that are difficult to predict, or impossible to predict.
        * Reactive to user input (eg. GUI apps)
    * Minimise state.  Concentrate it in one place.  State is the main source of complexity (unreadability), so minimise state to minimise complexity.  But don't reduce state beyond the point at which complexity starts to _increase_ again.  Don't add stupid complexity in order to completely eliminate state (eg. by using lunatic functional programming techniques like recursion and 'monads'.)

10. Separate Input/Output from Computation.

11. Separate Business Logic from Mechanical Work.

12. Centralise the Concern of Logical branching.  For maximum readability, the same logical branch should occur as few times as possible.  Antipattern: Doing the same logical check many times in the code.  There may be a tradeoff with redundancy.

13.  Coupling. The tricky bit.  Vague notions of 'decoupling', 'reusability', 'extensibility', etc can result in architectures that have overly convoluted coupling.  To try to make sense of this complex topic, we shall start with a taxonomy of different ways coupling can be done.

14. A Taxonomy Of Coupling.
    Idea about abstraction levels of coupling:
    * All components in same file.
    * Some components imported.
    * Some components injected, requiring an Outside Orchestrator.
    
    Idea about 'orders' of coupling:
    * Simple:  Calling As Connection.
    * Complicated:  Connection Before Calling.

    Concrete Types of Coupling.  How one code component uses another code component.
    * Function call.
    * Function call of injected function.
    * Method call on class.
    * Method call on injected object.
    * Object instantiation, then method call on object.
    * Inheritance.  Method call on parent class.

15. Interfaces: Coupling in Action.
    * Possible Rule:  "Only inject interfaces."  What did I mean by this?  I came up with _something_ like this late at night.  Need to think about this.
        * I _think_ I meant that code is hard to read if the injected function (or object) is completely unrestricted and could be _anything_.  Injection is better if the injected function could be one of several functions, but they all do the _same kind of thing_, in some sense.  In other words, injection is easier to understand if the injected code conforms to some kind of _interface_ or contract, and the more concrete that interface specification, the better.
    * Possible Rule:  Interfaces are abstract, by definition.  But make them as _least abstract_ as possible.  A cardinal rule of good prose writing is "be as concrete as possible".  Code writing is no different.
    * Trickiest bit:  Creating an interface that is simple _and_ can be cleanly extended.  If a concern has been cleanly separated, then the interface should be easy to design.  Conversely, a clunky interface strongly indicates a badly-abstracted Concern.
      * Consider using a Spec object to simplify complex function interfaces.  This means the function interface does not have to change.
    * API design.  Ideally: Atomic, and Multi-granular.  So _anything_ can be done by combinations of atomic calls, but a routine high-level task is a single easy call.
