+++
title = "Principles Of Code Structure"
date = 2022-12-19
weight = 10
+++


# "What the hell does this code do?" - Readability

Let's start with a very common everyday challenge that a developer faces:  You are working with an unfamiliar code base, and you have to use some function or object.  The immediate question is:

"What the hell does this do?"

Perhaps the function is part of an API; in any case it is the entry point into the code, and also the entry point of our discussion here.

The question "what the heck does this do?" gives us a good basis from which to define readability.

**Definition:  READABILITY:**  The (inverse) time taken to satisfactorily answer the question "what does this do?"  The most readable code takes the least amount of time to understand.  Unreadable code takes a long time to understand.

Obviously, we need to be comparing apples with apples:  We are considering different ways of coding the *same functionality*.  From the same entry point, there are an infinite number of different ways of implementing the same functionality.  Our concern is ranking those different ways by how long they take to understand - to rank them by readability.

Equally obviously, there is a subjective element.  Different developers are accustomed to different coding styles.  Developers vary enormously in their experience and exposure to code.  People will insist that things are "a matter of taste."  So, we are interested in principles of readability that are universal, in the sense that most reasonable people will agree.  We cannot account for the absurd opinions of highly non-neuro-typical outliers, so we won't bother.  What we seek are reasonable, defensible principles that are helpful in the vast majority of situations.

It is widely recognised that professional software engineers spend much more time _reading_ code than they do _writing_ code.  Put another way, over the lifetime of a piece of computer code, vastly more engineer-hours will be spent reading that code than the hours that were spent writing that code.  Since the time of a software engineer is expensive, it follows that making code as readable as possible is the best way to minimise engineering costs in the long term.

In rare circumstances, the speed of executing the code may be of paramount importance.  In that case, it makes sense to sacrifice readability for significant gains in speed.  However, such sacrifices of readability should be localised to the critical areas that affect execution speed - the rest of the code base should still be made as readable as possible.  Furthermore, experienced engineers note that the most readable code is often the fastest, because one essential element of readability is the elimination of redundant, unnecessary constructions.

### What about 'extensibility'?

A lot of unreadable code was written with the intention of being 'extensible'.  In fact, 'extensibility' was probably the dominant motivation in much programming advice from the 1990s onwards.  Object-oriented Programming, in particular, carried the (false?) promise of 'reusable, extensible, maintainable' code.  However:

1. In order to extend a piece of code, one must first understand it.  So the total time required to extend the code must include the reading time.  Thus, code that was written to be 'extensible' but is difficult to read, will take longer to modify than readable code that _technically_ requires slightly more work to modify.

2. Code that is easy to extend tends to have a very modular structure, with minimal coupling.  Happily, those are properties of highly readable code also.  Thus, code that is highly readable tends to be highly extensible.

3. You Ain't Gonna Need It (YAGNI).  Don't Solve Tomorrow's Problems.  Premature Optimisation is the root of all evil (_Knuth_ 1974). Because:
    * What is the best time to design a system for extensibility?  Answer: at the time you actually have to extend it.  Only at that point do you have the maximum possible information on the problem.   At any earlier time, you have less information, so will likely make worse engineering decisions.

4.  However, Don't Create Tomorrow's Problems.  If you **know** that your code will need to be extended, then that is in fact a specification for the design of the code.  Therefore, choose the most readable solution that meets the need for extensibility.  But keep in mind the previous point, and consider delaying the re-design for extensibility until the time you actually extend it.

Don't solve tomorrow's problems, but don't create tomorrow's problems, either.

Readability is King.  Except in rare circumstances when speed matters, optimise for readability.



# Elementary Code Structures

This _Principles Of Code Structure_ is not intended for complete beginner programmers.  Nevertheless, to prevent any possible confusion, we shall describe the two most common structural elements found in most modern computer languages.

### Functions
In earlier languages, they were also known as 'subroutines' or 'procedures'.  While subtle distinctions may be claimed between subroutines, procedures, and functions, modern usage has seemed to settle on a conception of function that is allied as closely as possible with the mathematical definition of a function.

A **function** in a programming language is a self-contained piece of code, that optionally takes some inputs, does some actions, and optionally returns an output.

### Objects
While the original conceptions of objects came out of Object-Oriented Programming, structures equivalent to objects are now available in most professional languages.  (For example, the functional programming language Clojure has 'Records' which work like objects.)

An **object** in a programming language is a single 'container' data structure, that may hold many different kinds of data, and may also have functions that are attached in some way to that data structure.  The key feature is that the functions - typically called 'methods' - can be accessed _via the data structure_ in the syntax of the language.


# The Art Of Abstraction

The English word 'abstract' is derived from the Latin word _abstractus_, meaning 'pulled away from'.  (The Latin particle _abs_ means 'away', and one may recognise 'tract' inside words like 'traction' and 'tractor', and see some connection to pulling.  A farm tractor _pulls_ a plough.)

The first use of _abstract_ in Middle English was as a noun to describe the _summary_ of a longer text.  This usage is still standard in papers published in scientific journals, which nearly always have an Abstract at the start of the paper that summarises the key findings.  The other main usages of the word _abstract_ are 'non-material, not concrete' and 'general, not specific'.  (There is also Abstract Art, which does not depict physical, material things (and is usually bloody awful).)

From the point of view of philosophy, the art of abstraction is an essential tool in the scientific method.  It is therefore also an essential tool in engineering.  To begin explaining _how_ abstraction is so useful, we shall start with this definition:

**To Abstract:** To pull out the _essential_ elements of something.

A corollary is that abstraction is the art of _ignoring the irrelevant_.  We identify what is important, and ignore the rest because it does not matter to our intellectual context.

The great power of abstraction comes from the fact that a single concrete entity can be abstracted in _different ways_.  There are _many different abstractions_ to be made from a single thing.

**Example:**  Consider an apple.  There are many _different_ 'essential' things that we can identify about the apple.  Which elements we consider to be essential is a choice, that will depend on what we care about in the relevant intellectual context.  Here are some elements of an apple, each of which could be considered the 'essential' element, depending on the intellectual context:
* It is coloured red.
* It is approximately spherical.
* It is edible.
* It is a member of the plant kingdom.
* It has a lifespan measured in weeks (without special cold storage).
* It is traded internationally.
* Its retail price contributes to the Consumer Price Index measure of inflation.
* _Et cetera_.

By abstracting from a concrete apple in these ways, we naturally tend to think in terms of _categories_ or _sets_.  An apple is _is in the set of_ red things.  An apple is _in the set of_ plants.  _Et cetera_.  Categorical or set-based thinking is very natural to people with sufficient education in mathematics.  In the modern world, primary school children learn the Venn diagrams of set theory.  And the extension into formal Boolean algebra and propositional calculus may be encountered in the first year of university.

### Categories: Abstractions In Common

As alluded to in our mention of _sets_ above, if we abstract the _same thing_ from two _different_ concrete objects, we have found something that is _common_ to both.  For example, an apple is a plant, and a cactus is a plant; both belong to the set of 'plants'.  Furthermore, an apple is edible, and a fish is edible; both belong to the set of 'edible things'.

So abstraction allows us to make connections between disparate things that are deeper than the immediate concrete connections.  An example of a merely concrete connection: an apple and an orange may both be in the same fruit bowl.  This connection _is_ an abstraction ('set of things in this fruit bowl'), but it is mere association, and we would scarcely think of it as abstraction.

### Hierarchies Of Abstraction

Abstraction can be applied to abstractions themselves.  For example, the abstraction 'fruit' defines a set including things like apples and oranges.  And the abstraction 'flowers' includes things like tulips and roses.  Moreover, the sets 'fruit' and 'flowers' are both _plants_.  Qualities that define plants can be abstracted from both fruit and flowers.

Hierarchies of abstractions can be constructed: sets of sets; sets within sets.

The value of such set hierarchies is that they underpin logical inference.  A classic illustration is the logical syllogisms formalised in Ancient Greece: "All humans are mortal.  Socrates is a human.  Therefore, Socrates is mortal."  Various other logical rules have also been formalised.

### The Power Of Abstraction

Abstract reasoning lets us find hidden connections between concrete observable things, and derive new information by using logical inference.  This allows us to make predictions about the world.  Science is essentially the systematic application of abstract reasoning.  Engineering can be viewed as a scientific approach to building things -- such as software.

'Intelligence', broadly speaking, could be described as the ability to abstract the essential elements of a situation and apply logic to them to derive new knowledge.

Abstraction lets us impose a structure on the universe that allows us to make sense of it.  With careful effort, we can construct a tree-like structure of concepts and categories that best allows us to understand a problem.  And we can construct _other_ conceptual hierarchies of the same physical situation, in order to look at the problem in a different way.

### Concrete-bound thinking: The Flynn Effect

An important point is that abstract reasoning is _far from universal_.  People with the privilege of a Western-type education in the 21st century use some degree of abstract reasoning all the time, and usually take it for granted that everybody always uses it and always has.  This is not true.  We have hard data on this, from research on the Flynn Effect of psychology.

**Flynn Effect:**  The discovery by New Zealand academic James Flynn that humans are getting smarter:  The IQ scores of the population are increasing over time.  The main cause of this seems to be that modern humans have been exposed to abstract reasoning through their education, and are thus better equipped to answer the logical reasoning questions in an IQ test.  How does this compare to the reasoning of uneducated people?  Consider these questions posed to illiterate peasants in Soviet Uzbekistan in the 1930s.  They went something like this:

Question: "There are no elephants in Germany.  Berlin is the capital of Germany.  Are there elephants in Berlin?"\
Peasant: "I don't know, I've never been to Berlin.  But if Berlin is a big city, they might have elephants there."

The modern mind would see this a failure to use set theory or logical inference.

Another type of question lists some objects, and asks for the connection between them.

Question: "Consider a dog and a rabbit.  What do they have in common?"\
Peasant:  "You use a dog to hunt rabbits."

The modern mind would think that the 'correct' answer is "They are both mammals", and consider the peasant to be thinking at the lowest possible level of abstraction - mere association.

It would be easy to mock these peasants for their lack of sophisticated reasoning.  But that would be utterly unfair.  In fact, primitive peoples have an _encyclopaedic_ knowledge of their environment, and a sharply-tuned operational intelligence that promotes their success in that (often-harsh) environment.  Such people never need abstract reasoning, and see it as useless word games.


### Risks And Failure Modes Of Abstract Thinking

#### Correct Abstractions

Scientific knowledge consists of elaborate conceptual structures that accurately map to the real world, and are internally consistent.  The key distinction that makes a concept 'scientific' is that it has been _tested by experiment_.  Abstractions are formulated, and eventually confirmed (or falsified) by experiments in the real world.
  * For example, the subatomic particle known as a _quark_ started out as a purely mathematical abstraction that simplified and clarified the theory of subatomic particles.  But much later, high-energy physics experiments confirmed the physical existence of quarks.

But if our abstractions cannot be tested with the rigour of science, then how do we decide if they are 'good' or not?

The answer to this question is deep, and beyond the scope of this essay.  Only some rough guidelines can be suggested:
  * A good abstraction **simplifies** our understanding of the situation.
  * A good abstraction **unifies** various disparate elements, that were previously seen as having no relation.
  * A good abstraction will tend to be **generally applicable**, to a wider problem space beyond the current problem.  It may have __predictive power__.
  * A good set (or hierarchy )of abstractions will be **internally consistent**.  There will be no contradictions.

Thus, abstract reasoning is actually very risky, in the following sense: It can be done very badly, leading to a false understanding of the universe, and that false understanding may persist for a very long time, because of the difficulty of testing it.  Enormous amounts of time and energy may be wasted on building castles in the air, discussing how many angels may dance on the head of a pin.

Primitive people don't suffer much from this problem, because errors in concrete thinking are usually immediately visible.  "Trust me, there are no bears in this cave!"  _Chomp_.  But it doesn't take much additional cultural sophistication to suffer badly from it.  "We need to throw a virgin into the volcano to prevent it from erupting".  _"Aaaaargh!_"  Silence.  "See, it's working."

#### Correct Level Of Abstraction

Given that _hierarchies_ of abstractions may be constructed, it is critical to choose the abstraction at the _right level_ for the problem.  The correct level of abstraction is this: **as concrete as possible** (but no more).  In other words, choose the abstraction that is the _least abstract_ that you can get away with.

A little-publicised but absolutely fundamental rule of good prose writing (and good communication in general) is to use the lowest possible level of abstraction (but no lower).  Think about it: a concrete concept is more precise, explicit, and easy to understand than a vague generality.  **The same applies to writing computer code.**

As an aside, overly abstract language may be _deliberately_ employed by people not wanting to commit to any specifics, or more nefariously, by people trying to give the false impression they know what they are talking about.

When a person reaches the level of intellectual maturity at which they can start using abstract language, they may take delight in using it as much as possible.  This irritating phenomenon often appears in the early teens, and some people never grow out of it, wrongly believing that overly-abstract language is a sign of intelligence.  At its worst, it manifests as the use of multiple high-level abstractions to triangulate on the concrete; the specific object is the intersection of several sets.  For example: "Manual excavation implement" is the intersection of 'set of things operated by hand', 'set of things related to digging', and 'set of tools'; in other words, a _spade_.  Don't be a wanker, call a spade a spade.

The point is that rational, abstract thought is _difficult and unnatural_.  But is is an essential skill for software engineering.  One needs careful, disciplined thinking to develop this skill.  Make no mistake, Uzbek peasants _suck_ at programming.


## Abstract Reasoning in Software Engineering

The preceding section on the art of abstraction contained rather a lot of philosophical material, none of it directly concerned with programming.  The reader may be surprised at this.  But there is a motivation:  The word _abstraction_ is used _all the time_ in software engineering, very often without much depth of understanding.  This book strives to help with this.

In practice, abstraction in software engineering works like this:
1. The problem domain is analysed, and broken into different entities, by identifying fundamental elements and abstracting out various actions, responsibilities, _etc_.  The relationships between the various entities give rise to a (probably hierarchical) structure.
2. In general, each separate entity is created as a separate module of computer code.  The separate modules are connected together to reflect the relationships between the abstract entities.

Your computer code will live or die depending on the quality of your abstractions.  Abstractions come to life as the very components and structures of your code, the architecture itself.  Once the code has been written and is in use, it can be _very hard_ to change the structure.  Therefore, it is _very important_ to spend the effort finding good abstractions, because a hastily-conceived bad abstraction may become a burden that you are permanently stuck with.  The wrong abstractions can _f@*$ you up_.

This book is in a large part a guide to abstractions that have proven useful - a guide to various elements of computer code that have turned out to be essential.

### Information Hiding

In software engineering, abstraction often results in _information hiding_.  Consider this: Some lines of code are seen to be all related to the same abstract thing, so the code is pulled out into a separate module (function or object).  The module _name_ describes the abstraction, and the _details_ are _hidden away_ inside the module.  At the point in the code where the new module is used, the abstraction is reified as an explicit module name, and the irrelevant details are hidden.

For more discussion, see the chapter below on Separation Of Complexity.

Not all abstractions involve information hiding.  An essential aspect of the code may be pulled out into its own module, but nothing is hidden.  All elements are simply accessible from a single coherent module.  (See definition of coherent in chapter on Separation Of Concerns.)

### Malabstractions

Since both abstract reasoning and software engineering are difficult and unnatural (and in the case of software engineering, _unwholesome_), standard errors in abstraction abound.  Here we examine some commonly-observed errors in abstraction (or 'malabstractions', to coin a term).

1. Making the _wrong_ abstractions.
2. Using the _wrong level_ of abstraction, usually _too high a level_ of abstraction.
3. Abstraction Addiction 1.  Making things as abstract as possible, i.e. as general as possible.
4. Abstraction Addiction 2.  Abstracting out _everything_ that can be.  (See DRY below.)
5. Adding useless layers and wrappers that do not actually provide any abstraction, because they do not hide irrelevant detail, just pass calls through.
6. Peasant abstraction.  Creating a module that is a tangle of disparate elements that are merely associated somehow.


#### DRY is bad advice

A ubiquitous piece of advice given to beginner programmers is "Don't Repeat Yourself".  So beginners assiduously pull out _every_ instance of repeated code and create an abstraction for it.  Now, for a given piece of repeated code, this _may_ be the correct thing to do. Or it may not.

There are two rules that should be followed when applying DRY:
1. A little repetition is better than the wrong abstraction.
2. A _lot_ of repetition is still better than the wrong abstraction.

Be careful; don't blindly follow DRY.  The point is **not** "Don't Repeat Yourself", the point is "The right abstractions massively improve your code, so search carefully for them".

(The opposite of DRY is WET, which is alleged to mean either "Write Everything Twice" or "We Enjoy Typing".  WET is obviously _terrible_ advice.  But the joke shouldn't be taken as support for dogmatically applying DRY.)

#### Peasant Abstraction

Creating a separate module of code that contains a tangle of disparate elements with only some loose association with each other, and proudly calling it an 'Abstraction'.  Typically, the abstraction implicitly defines "the set of all the things I might need to do this thing".  As noted above, this is barely an abstraction at all - it is mere association.

Obviously, the art of abstraction should be applied to the tangle of disparate elements within the module, and to the module itself in the context of the wider code base.  It is likely that the entire module itself should not exist.


# The Twin Pillars: Separation Of Concerns and Clarity Of Coupling

The central skill of software engineering is to analyse the problem to figure out what the different aspects are, and how those aspects relate to each other.

More precisely, an 'aspect' of a programming problem is an _area of concern, or responsibility_ that can be abstracted from from it.

The first pillar of software engineering is to _separate the concerns_ into separate software modules (generally, functions or objects).

The second pillar of software engineering is to decide how the separate concerns will be connected.

The separated concerns and the coupling between them are two sides of the same coin.  They define the totality of your software architecture.  Deciding on what the concerns are and how they connect is what software architecture _is_.

## Platinum Rule Of Thumb

Break computer code into separate modules such that:
1. Each module deals with a single concern or responsibility.
2. The coupling between the modules is minimised.

To add more nuance: The coupling between modules should be made as clear and obvious as possible.  This is _often_ achieved by minimising the amount of coupling.

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

### Collation Of Concerns (Single Concern In A Single Place)

We have established the value of a single module of code only dealing with a single concern.

The complement to that is to pull all the code that deals with the same concern into a single module of code.  In other words, _collate_ all the code that deals a single concern, and put it in a single module.

This also makes the code easier to understand.  A single responsibility is in a single place.  The code is also much easier to modify - only a single place in the code needs to be touched.

This principle tends to apply more to refactoring existing code (or prototypes).  Code that is well-designed from scratch will automatically tend to have a single concern in a single place.

### Coherence

A piece of code may be described as **coherent** if all of its lines of code relate to a single concern.  A module of code is 'incoherent' if some of its lines of code relate to one concern, and other lines relate to a different concern.

Coherent modules of code are the _consequence_ of correctly separating concerns.

### Summary: Separate Concerns; Collate Concerns
1. A single module of code should deal with a single concern.
2. A single concern should be dealt with in a single module of code.


A number of concerns have been identified that appear time and time again in many computer programs.  Appropriately separating those particular concerns should be the first order of business when designing a software architecture.  Details follow in the next several chapters.

# Separate Inherent Complexity from Collateral Complexity

There are various definitions of the 'complexity' of a computer program, some highly mathematical, but for our purposes, it suffices to employ common-sense notions along the lines of 'complexity = amount of stuff, and amount of connections between stuff'.  More complexity is obviously harder to understand.  A key focus of good software engineering is managing complexity: disentangling it, and minimising it.

Complexity can be broken into three different types:

### Inherent Complexity

Inherent complexity is the complexity of the actual domain problem itself.  It may be the complexity of a mathematical algorithm, or the complexity of some business logic, or the complexity of managing a long-term interaction with a user.

Inherent complexity cannot be reduced, because it is inherent to the domain problem itself.

### Collateral Complexity

Collateral complexity is the complexity in the details of the solution to the domain problem, that is not inherent to the problem.  This is best explained with an example:

Suppose the domain problem requires saving some data to a database.  The action 'save data to database' is considered part of the _inherent complexity_ of the problem, because it is a critical step in the algorithm.  But the _details_ on how to connect to the database, where the passwords are stored, the exact protocol for calling a Postgres database, _et cetera_, are considered to be only _collateral_ complexity, because these low-level details do not fundamentally matter to the solution.  This collateral complexity is essential to solve the domain problem, but it is not _inherent_, because the details could change quite drastically (for example, by changing to a different database) without affecting the operation of the solution.

### Accidental Complexity

Accidental complexity is any complexity in the design that is _not_ essential to solve the domain problem.  The problem has an inherent complexity, and there is the collateral complexity of the low-level details _required_ to solve the problem, and any remaining complexity is essentially due to _bad design_.

Classic examples include: poor use of Object Oriented design, unstructured spaghetti code, having the wrong abstractions, confusing or obscure variable names, 'clever' code that is more generalised than it needs to be, _et cetera, et cetera, ad nauseum_.

The point about accidental complexity is that is _can_ and _should_ be eliminated.  In this sense, it is completely different from collateral complexity, which _cannot_ be eliminated.

### Notes

Separating inherent complexity from collateral complexity is a good example of the art of abstraction at work, and one of the first abstractions that novice programmers naturally tend to start doing.  Pulling the boring details of a database connection into a _separate function_ is an excellent and easy first step towards a better program structure.  Several lines of code are recognised to be all contributing to the same _abstract_ activity - 'save to database' - and are not part of any other concern.  Therefore, this Concern is separated out into its own function.  Engineers would often describe this with language like "abstracting out the database connection."

A corollary is that the function call `save_to_database()` is at a higher level of abstraction, and that level of abstraction is inherent to the problem solution.  An _essential_ step of the solution algorithm has now been made explicit with a self-documenting function name.  The code is now easier to understand; it is more readable.

In summary:
1. Separate Inherent Complexity from Collateral Complexity.
2. Eliminate Accidental Complexity.  Or at least understand the trade-offs.


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


# Distinguish Algorithm-like Code From Data-like Code

This principle is in many ways an expansion and restatement of the previous principle 'Separation Of Functions And State', though typically applicable at a higher level of abstraction.

Time is linear.  Time is just one damn thing after another.

Important Corollary: The execution of a computer program is a _sequence_ of operations, one after the other.  We can say that program flow is _linear_.

Even more important corollary:  Reading is a linear process.  We read one element at a time, _incrementally_ building an understanding of the whole piece.

Thus, to answer "what does this code do?" is to understand the sequence of operations during the execution of the code.  Furthermore, our understanding of that sequence of operations is built by reading parts of the code, one after the other.

Now, a computer program _as a whole_ has an execution order, a program flow.  However, not all parts of the program may have a meaningful execution order.  For example, code that is some kind of data structure is essentially static, and merely accessed by other code, and so does not really have a meaningful execution order.

If code _does_ have a meaningful execution order, then we can describe it as **'algorithm-like'**.  An algorithm is colloquially described as a 'recipe', or sequence of steps to carry out.  So code that is essentially a recipe of steps to execute in order, is algorithm-like.

Code that is _not_ algorithm-like may be described as **'data-like'**.  As mentioned, this tends to be static structures that don't really _do_ anything, just store information to be accessed by other parts of the code.

Note that algorithm-like code may still contain _state_.  An algorithm may work by mutating some state, so that state is an integral part of the algorithm.  We cannot apply a simplistic hard-and-fast rule like "State = Data-like; Pure Functions = Algorithm-like".  Rather, the point is to distinguish the _role_ of state - is it to serve an algorithm?  Or is it more like reference data?

As we become familiar with the distinction between algorithm-like and data-like code, we can see situations where they should be _separated_.  This point is best illustrated with an example such as the following.

### Antipattern: Objects Conflating Algorithms And Data

A common bad construction is an object that:
1. Stores input parameters as object variables.
2. Executes an algorithm, using object variables as temporary working variables.
3. Stores the output of the algorithm as yet more object variables.

Faced with this abomination, the reader thinks:  What is the class doing?  Executing an algorithm?  Storing the result of the algorithm?  Storing the algorithm inputs as a kind of specification?  Are some variables merely irrelevant temporary working variables?  Depressingly, the answer to all of the above is "Yes".

A toy example of this antipattern in Python:
```py
class Rotundicity:

    def __init__(a, b, c):
        self.a = a
        self.b = b
        self.c = c

    def discombobulate():
        self.p = self.a**self.b + sin(self.c)/cos(self.a)

    def freneticise():
        self.q = exp(a, p) + 3.141592654 * self.p * arctan(self.b/self.c)

    def compute():
        self.rotundicity = log(self.p) - log(self.q) + self.p**2 + self.q**3

    def q_factor():
        return (self.a + tan(self.b))/self.rotundicity
```

Consider the stupid example above.  By just reading the class definition, it is impossible to know the _purpose_ and usage of the code.  It seems clear that `rotundicity` is an important thing to be computed, but why is it stored on the class?  Will it be recomputed again at random times?  Are `p` and `q` important?  If not, why are they accessible attributes on the class?  Would a user ever set `p` or `q` directly?  _Et cetera_.

Now, some of the problems with this class could be alleviated if the language had 'private' class member variables, _etc._  (Python does not.)  However, there are fundamental _structural_ problems with the code that should be addressed.  We need to _separate concerns_.  Distinguish the _input data_ from the _algorithm_ from the _output data_, and separate them.  A possible refactoring is as follows:

```py
class RotundicityInputs:
    def __init__(a, b, c):
        self.a = a
        self.b = b
        self.c = c


class Rotundicity:
    def __init__(rotundicity, q_factor):
        self.rotundicity = rotundicity
        self.q_factor = q_factor


def compute_rotundicity(data: RotundicityInputs):
    p = discombobulate(data)
    q = freneticise(data, p)

    rotundicity = log(p) - log(q) + p**2 + q**3
    q_factor = (data.a + tan(data.b))/rotundicity

    return Rotundicity(
        rotundicity=rotundicity,
        q_factor=q_factor,
        )


def discombobulate(data: RotundicityInputs):
    return data.a**data.b + sin(data.c)/cos(data.a)


def freneticise(data: RotundicityInputs, p: float):
    return exp(data.a, p) + 3.141592654 * p * arctan(data.b/data.c)
```
Now it is very clear that `rotundicity` and associated `q_factor` are the outputs that matter.  They are tied together on a simple, lightweight data class, that can be passed around the rest of the program.  It is equally clear that the only parameters that a user can control are `a`, `b`, and `c`.  Finally, the actual algorithm for calculating the outputs from the inputs is now crystal clear.

An alternative refactoring would be to have the `compute_rotundicity()` function be a _method_ on the `RotundicityInputs` class.  This might be a more appropriate structure if the `RotundicityInputs` data class is _state_ that changes frequently, and the rotundicity needs to be computed frequently.

## Enforce Consistency Of State

In the stupid example above, the lack of separation of concerns causes another more subtle but potentially more serious problem: the state can become inconsistent.  Here is how:  There is only _one_ value of `rotundicity` that is mathematically consistent with given inputs `a`, `b`, and `c`.  However, the input variables can be modified _without_ updating the output variables.  Thus, since the 'state' of the `Rotundicity` object consists of all five variables, the state can become inconsistent.

This is better illustrated with a simpler example.  Consider this snippet of code that represents geometric shapes drawn on the screen:
```py
class Circle:
    def __init__(x: float, y: float, r: float):
        # Position on screen.
        self.x = x
        self.y = y

        # Radius
        self.r = r

        self.calculate_area()  # Sets self.area

    def calculate_area()
        self.area = 3.141592654 * self.r ** 2
```
The problem is that both `r` (radius) and `area` are attributes of a `Circle` object, and radius `r` can be updated _without_ updating `area`.  Thus, the state of the `Circle` object can become inconsistent.

There are at least a couple of fixes.  Probably the best way to enforce consistency of state is to **minimise state**, and not store `area` as state at all - just compute it when needed, in the spirit of functional programming.  The code would look like this:
```py
class Circle:
    def __init__(x: float, y: float, r: float):
        # Position on screen.
        self.x = x
        self.y = y

        # Radius
        self.r = r

    def calculate_area()
        return 3.141592654 * self.r ** 2
```
This is a very clean solution, that keeps code minimal and easy to understand.

Another approach to enforcing consistency of state is to use 'setters', in the spirit of traditional object-oriented programming.  This approach is automatically re-calculate `area` every time radius `r` is changed.  The following code is not idiomatic Python, but illustrates the approach:
```py
class Circle:
    def __init__(x: float, y: float, r: float):
        # Position on screen.
        self.x = x
        self.y = y

        # Radius
        self.set_radius(r)

    def set_radius(r: float):
        self.r = r
        self._calculate_area()

    def _calculate_area()
        self.area = 3.141592654 * self.r ** 2
```
(There is an idiomatic Python way to define setters, but the syntax will be less clear to readers not familiar with this somewhat obscure Python feature.)

The disadvantage of this approach to enforcing consistency of state is that area _must_ be calculated every time the radius is changed, even if we don't care about the area at the time.  This doesn't matter for this minimal example, but in real-world code, there could be a significant performance cost to automatically doing a costly calculation regardless of whether or not it is needed.  Thus, in general, prefer the simpler method of _minimising state_, to enforce consistency.

# Separate Input/Output From Computation

A lot of computer code follows the pattern handed down to us from the ancients:
1. Get some data from somewhere.
2. Do some computations from the data to produce new data.  Equivalently, _transform_ the data.
3. Put the new data somewhere.

Separate the code that does Input or Output into its own modules.  Do _not_ make an I/O call in the middle of some code that is doing a computation.

An Input code module deals with things like reading a configuration file, reading environment variables from the operating system, loading data from a file, _et cetera_.

An Output code module will typically handle writing to a file or database, or transferring data through a network call.

Rules of thumb for readable code:
1. Try to put the calls to the Input module at the beginning of the program.
2. Try storing the input data in some kind of State module, for later use.
3. Try to put he calls to the Output module at the end of the program.

Input and Output are major dependencies of the program.  For example, a program may depend on the existence of a config file as input.  Now suppose the config variables are not needed until half way through the program.  An 'efficient' programmer might delay reading the config file until the point at which it is needed.  However, it is better to read the config file at the very beginning of the program, because:
1. It makes the dependency on the existence of the config file immediately explicit to the reader.
2. If the file is missing, the program will error immediately, instead of wasting time on a computation that will ultimately fail.

Make dependencies explicit.  Declare them early; your readers will want to know about them.  Fail early.  Make sure you have everything that you need before starting the job.


# Separate Business Logic From Mechanical Work

Business logic is the _whole point_ of software.  Software is engineered to solve business problems.

Therefore, in your code, _highlight_ the business logic.  Try to elevate it to its own module so that the business logic is _obvious_.  This also tends to make it easier to modify the business logic.

Code is often read for debugging purposes, or to answer a question about system behaviour that is not documented.  These are issues of business logic: "What is the system supposed to do, and is it actually doing it?"  Therefore, make life easy for everybody by making business logic extremely explicit, sitting by itself in an easy-to-find place.  Keep it _separate_ from low-level mechanical details about _how_ the system implements that business logic.

Deciding what counts as business logic may not always be easy.  But try to keep this separation in mind when designing the system.  This abstraction is one that _matters_.


# Collate The Concern Of Logical Branching

If your code requires a logical branch, try to do it only once.  Your code will be much cleaner and easier to read.

Making the _same_ logical branch (i.e. exactly the same logical conditions) in _multiple_ places should be considered an anti-pattern, or at least a code smell.  The resulting code is always cluttered and messy.  Try to refactor it to have only one occurrence of the logical branch.

In graphical form, the left hand pattern is much easier to understand than the right hand pattern:

<div align="center">
<svg width="600" height="640">
    <line x1="100" y1="20" x2="100" y2="120" stroke="red" stroke-width="8"/>
    <line x1="100" y1="120" x2="20" y2="220" stroke="red" stroke-width="8"/>
    <line x1="100" y1="120" x2="180" y2="220" stroke="red" stroke-width="8"/>
    <line x1="20" y1="220" x2="20" y2="620" stroke="red" stroke-width="8"/>
    <line x1="180" y1="220" x2="180" y2="620" stroke="red" stroke-width="8"/>
    <circle cx="100" cy="20" r="20" fill="blue"/>
    <polygon points="100,90 70,120 100,150 130,120" fill="lime" stroke="black"/>
    <circle cx="20" cy="220" r="20" fill="blue"/>
    <circle cx="20" cy="320" r="20" fill="blue"/>
    <circle cx="20" cy="420" r="20" fill="blue"/>
    <circle cx="20" cy="520" r="20" fill="blue"/>    
    <circle cx="20" cy="620" r="20" fill="blue"/>    
    <circle cx="180" cy="220" r="20" fill="blue"/>
    <circle cx="180" cy="320" r="20" fill="blue"/>
    <circle cx="180" cy="420" r="20" fill="blue"/>
    <circle cx="180" cy="520" r="20" fill="blue"/>
    <circle cx="180" cy="620" r="20" fill="blue"/>
    <line x1="500" y1="20" x2="500" y2="120" stroke="red" stroke-width="8"/>
    <line x1="500" y1="120" x2="420" y2="220" stroke="red" stroke-width="8"/>
    <line x1="500" y1="120" x2="580" y2="220" stroke="red" stroke-width="8"/>
    <line x1="420" y1="220" x2="500" y2="320" stroke="red" stroke-width="8"/>
    <line x1="580" y1="220" x2="500" y2="320" stroke="red" stroke-width="8"/>
    <line x1="500" y1="320" x2="500" y2="420" stroke="red" stroke-width="8"/>
    <line x1="500" y1="420" x2="420" y2="520" stroke="red" stroke-width="8"/>
    <line x1="500" y1="420" x2="580" y2="520" stroke="red" stroke-width="8"/>
    <line x1="420" y1="520" x2="500" y2="620" stroke="red" stroke-width="8"/>
    <line x1="580" y1="520" x2="500" y2="620" stroke="red" stroke-width="8"/>
    <circle cx="500" cy="20" r="20" fill="blue"/>
    <polygon points="500,90 470,120 500,150 530,120" fill="lime" stroke="black"/>
    <circle cx="420" cy="220" r="20" fill="blue"/>
    <circle cx="500" cy="320" r="20" fill="blue"/>
    <polygon points="500,390 470,420 500,450 530,420" fill="lime" stroke="black"/>
    <circle cx="420" cy="520" r="20" fill="blue"/>    
    <circle cx="580" cy="220" r="20" fill="blue"/>
    <circle cx="580" cy="520" r="20" fill="blue"/>    
    <circle cx="500" cy="620" r="20" fill="blue"/>
</svg>
</div>

### Make Branching Explicit

One (misguided) way to save a line of code is to write a logical branch like this:
```py
x = 0  # Default value.
if some_condition is True:
    x = 1
```
Now, does this _look_ like a logical branch?  At first glance, the reader notices that a variable is set, then mutated _if_ a particular condition is true.  The pattern is: 1) Do some work. 2) If a condition is true, then _undo and redo_ the work.

What does mutating a variable have to do with logical branching?  The answer is: _nothing_.  This mutation is not necessary to achieve logical branching.  In fact, while all languages allow logical branching, there are modern languages with an emphasis on safety that strongly discourage mutation, or even forbid it.  (Eg. Rust, and functional languages.)  Mutation typically makes code harder to reason about, so should be kept to an absolute minimum.

The _meaning_ of the code is: make a binary logical choice.  Therefore, the code should reflect that meaning as directly as possible.  The traditional `if else` construction does this perfectly:
```py
if some_condition is True:
    x = 1
else:
    x = 0
```
The other benefit of the traditional `if else` is that the code at the same _logical level_ (down one branch or the other) is at the same _indentation level_.

In the diagrams below, the _meaning_ of the code is shown as the tree with red links, and the _execution flow_ of the code is shown as the black arrows.

<div align="center">
<svg width="600" height="260">
    <defs>
        <marker id="arrowhead" markerWidth="10" markerHeight="8" 
         refX="8" refY="4" orient="auto">
            <polygon points="2 4, 0 8, 10 4, 0 0"/>
    </defs>
    <-- Left hand tree -->
    <line x1="100" y1="20" x2="100" y2="120" stroke="red" stroke-width="8"/>
    <line x1="100" y1="120" x2="20" y2="220" stroke="red" stroke-width="8"/>
    <line x1="100" y1="120" x2="180" y2="220" stroke="red" stroke-width="8"/>
    <circle cx="100" cy="20" r="20" fill="blue"/>
    <polygon points="100,90 70,120 100,150 130,120" fill="lime" stroke="black"/>
    <circle cx="20" cy="220" r="20" fill="blue"/>
    <circle cx="180" cy="220" r="20" fill="blue"/>
    <text x="0" y="260">x = 0</text>
    <text x="160" y="260">x = 1</text>
    <--   Flow arrows -->
    <line x1="20" y1="0" x2="20" y2="195" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="43" y1="217" x2="95" y2="155" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="105" y1="155" x2="155" y2="215" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <-- Right hand tree -->
    <line x1="500" y1="20" x2="500" y2="120" stroke="red" stroke-width="8"/>
    <line x1="500" y1="120" x2="420" y2="220" stroke="red" stroke-width="8"/>
    <line x1="500" y1="120" x2="580" y2="220" stroke="red" stroke-width="8"/>
    <circle cx="500" cy="20" r="20" fill="blue"/>
    <polygon points="500,90 470,120 500,150 530,120" fill="lime" stroke="black"/>
    <circle cx="420" cy="220" r="20" fill="blue"/>
    <circle cx="580" cy="220" r="20" fill="blue"/>
    <text x="400" y="260">x = 0</text>
    <text x="560" y="260">x = 1</text>
    <-- Flow arrows -->
    <line x1="530" y1="0" x2="530" y2="115" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="527" y1="127" x2="580" y2="195" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
</svg>
</div>

The left-hand diagram of the code using mutation shows how the code actually traverses one branch of the tree _before_ encountering the conditional.  This disconnect from the semantics of the code has a cognitive cost.  So the 'shorter' method using variable mutation is actually harder to understand.  Don't try to save a single line of code at the expense of readability.  Just use the traditional `if else` construction.

### Use Polymorphism To Eliminate Logical Branching
Consider this code, a toy example of part of some kind of graphics program.  It may not be realistic, but it illustrates a point.
```py
class Square:
    def _init_(width):
        self.width = width


class Circle:
    def _init(radius):
        self.radius = radius


def calculate_total_area_of_shapes(shapes: list):
    total_area = 0

    for shape in shapes:
        if isinstance(shape, Square):
            total_area += area_of_square(shape)

        elif isinstance(shape, Circle):
            total_area += area_of_circle(shape)

        else:
            print("Shape not recognised.  Cannot calculate area.")

    return total_area


def area_of_square(square: Square):
    return square.width ** 2


def area_of_circle(circle: Circle):
    return 3.141592654 * circle.radius ** 2
```
The important point to note is the **logical branching** in the function `calculate_total_area_of_shapes()`.

This example code can also be considered a canonical example of the value of _method polymorphism_.  Let us rewrite the code to use method polymorphism.

```py
class Square:
    def _init_(width):
        self.width = width

    def area(self):
        return self.width ** 2


class Circle:
    def _init_(radius):
        self.radius = radius

    def area(self):
        return 3.141592654 * self.radius ** 2


def calculate_total_area_of_shapes(shapes: list):
    total_area = 0

    for shape in shapes:
        total_area += shape.area()

    return total_area
```
The code has been simplified considerably, and is easier to read.  This shows the value of method polymorphism.

But let's dig a little deeper.  Obviously, the two functions for calculating area have been _moved_ to be attached to the data structures they operate on. And the main function `calculate_total_area_of_shapes()` is drastically simpler because it no longer contains the logical branching.  Was it moved?  Upon inspection, the **logical branching** has apparently completely **disappeared** from our code!  Where did it go? In fact, the logical branching is still inside the compiled (byte) code in the form of look-up table or similar.  Method polymorphism has allowed us remove the logical branching from our source code, where it adds complexity for the human reader, and move it into the compiled code, where it is completely out of our sight, and now the responsibility of the computer.

Removing the complexity of logical branching from our source code is perhaps an under-appreciated aspect of object-oriented techniques such as this.


# Coupling

Now that we have separated all the concerns into separate modules, how should we connect them together?

There are two aspects to Coupling:
1. The types of actual connections.
2. How the connected modules together create an overall structure.

In keeping with our empirical, ground up, scientific approach, we shall start with a taxonomy of ways that two modules can be connected.

# Taxonomy Of Connections

Our goal in this chapter is to describe the different types of connection that may be used, and give some preliminary assessment on two attributes:
1. How simple they are to understand.
2. How easy they are to extend or modify, in particular, how easy it is to swap out one module for another.

The value of assessing Simplicity is obvious, since we usually value readability above all else.

There are a few reasons why we should assess Extensibility:

Firstly, suppose we **know** that the code will need to be modified in the future.  Then the specification for the code will include the criterion "Needs to be extensible".  So we choose the _most readable_ solution that provides the extensibility that we need.

Secondly, the label 'extensible' is often applied very vaguely.  Object-Oriented methods, in particular, are often claimed to be 'extensible', without much deep analysis as to how easy they actually are to extend, and whether they truly are easier to extend than simpler competing methods.  It is worth doing a little critical examination of this here.

Thirdly, 'swappable' modules must be loosely coupled, which tends to correlate with cleanly separated concerns.


### Types Of Connections

Some types of connection, in approximate order of simplicity.

1. Function call.
2. Method call on class.
3. Object instantiation, then method call on object.
4. Function call of injected function.
5. Method call on injected object.
6. Inheritance.  Method call on parent class.

###  Function Call

```py
def secondary(data):
    # Do stuff.


def main():
    ...
    secondary(data)
    ...
```
#### Simplicity:
As simple as possible.

#### Extensibility:
Assuming that an `alternative()` function has been written, then changing the coupling simply requires changing the function call in `main()`:
```py
# def secondary(data):
#     # Do stuff.


def alternative(data):
    # Do different stuff.


def main():
    ...
    # secondary(data)
    alternative(data)
    ...
```
* New function.
* One-line change in `main()`, to call new function.

### Method Call On Class

```py

class SomeStupidClass:

    @staticmethod
    def secondary(data):
        # Do stuff.


def main():
    ...
    SomeStupidClass.secondary(data)
    ...
```
#### Simplicity:
Almost as simple as possible.  The class simply acts as a _namespace_ for the `secondary()` function.  In some situations, having such a namespace may tidy up the code and make it more readable.

#### Extensibility:
This depends on whether the new alternative function lives in the _same_ namespace class, or needs its own new class.

Like this:
```py

class SomeStupidClass:

#    @staticmethod
#    def secondary(data):
#        # Do stuff.

    @staticmethod
    def alternative(data):
        # Do different stuff.


def main():
    ...
    # SomeStupidClass.secondary(data)
    SomeStupidClass.alternative(data)
    ...
```

Or this:
```py

#class SomeStupidClass:
#
#    @staticmethod
#    def secondary(data):
#        # Do stuff.


class LessStupidClass:

    @staticmethod
    def secondary(data):
        # Do stuff better.


def main():
    ...
    # SomeStupidClass.secondary(data)
    LessStupidClass.secondary(data)
    ...
```
* New method or class.
* One-line change in `main()`, to call different class or method.


### Object Instantiation, Then Method Call On Object

```py

class SomeStupidClass:

    def secondary(self, data):
        # Do stuff.


def main():
    ...
    stupid_object = SomeStupidClass()
    stupid_object.secondary(data)
    ...
```

#### Simplicity:
Extra overhead of a container class, and instantiating the class.

#### Extensibility:
Swapping functionality requires either a new method on the existing class, or a new class.

Like this:
```py

class SomeStupidClass:

#    def secondary(self, data):
#        # Do stuff.

    def alternative(self, data):
        # Do stuff better.

def main():
    ...
    stupid_object = SomeStupidClass()
    # stupid_object.secondary(data)
    stupid_object.alternative(data)
    ...
```

Or this:
```py

# class SomeStupidClass:
#
#    def secondary(self, data):
#        # Do stuff.


class LessStupidClass:

    def secondary(self, data):
        # Do stuff better.


def main():
    ...
    # stupid_object = SomeStupidClass()
    stupid_object = LessStupidClass()
    stupid_object.secondary(data)
    ...
```

* New method or class.
* One-line change in `main()`, to call new method or instantiate new class.

### Function Call Of Injected Function

```py
def secondary(data):
    # Do stuff.


def main(injected_func):
    ...
    injected_func(data)
    ...


def orchestrator():
    ...
    main(injected_func=secondary)

```

#### Simplicity:
Not so simple...  There are now _three_ modules required.  However, each module is itself very simple.  A first-class function needs to be followed as it is passed around.  When reading the `main()` function alone, it is impossible to know what _real_ function the injected function actually is.  An IDE would probably be unable to 'jump to source' of `injected_func`.

#### Extensibility:
The defining attribute of this form of coupling is that the `main()` function _does not need to be touched_ to change functionality.

However, the _orchestrator_ function will need to be changed, to pass in the new function.

```py
# def secondary(data):
#    # Do stuff.


def alternative(data):
    # Do stuff better.


def main(injected_func):
    ...
    injected_func(data)
    ...


def orchestrator():
    ...
    # main(injected_func=secondary)
    main(injected_func=alternative)

```
* New function.
* `main()` function is **not** changed.
* One-line change in orchestrator function, to pass in alternative function.


### Method Call On Injected Object

```py
class SomeStupidClass:

    def secondary(self, data):
        # Do stuff.



def main(injected_object):
    ...
    injected_object.secondary(data)
    ...


def orchestrator():
    ...
    stupid_object = SomeStupidClass()
    main(injected_object=stupid_object)

```

#### Simplicity:
Relatively complex.  There are now _three_ modules.  There is the extra overhead of a container class, and instantiating the class.  An injected object needs to be followed as it is passed around, though this is arguably easier to understand than a first-class _function_ being passed around, since it is probably more commonly seen.

When reading the `main()` function alone, it is impossible to know which real class the injected object actually is.  An IDE will probably not be able to 'go to source' of `injected_object`.  This will be less of a problem if the injected object conforms to an _interface_, that can be specified as the type of the `injected_object` argument.

#### Extensibility:
Could in principle depend on whether the new functionality needs a whole new class or just a new method on the existing class.  However, the whole point of the flexibility of the orchestrator pattern is to _easily inject a different object_, so that's what we'll consider here.

```py
# class SomeStupidClass:
#
#    def secondary(self, data):
#        # Do stuff.


class LessStupidClass:

    def secondary(self, data):
        # Do stuff better.


def main(injected_object):
    ...
    injected_object.secondary(data)
    ...


def orchestrator():
    ...
    # stupid_object = SomeStupidClass()
    stupid_object = LessStupidClass()
    main(injected_object=stupid_object)

```
* New class with different method _of same name_.
* `main()` function is **not** changed.
* One-line change in orchestrator function, to instantiate new class.

### Inheritance

```py
class ParentClass:

   def secondary(self, data):
       # Do stuff.


class MainClass(ParentClass):

    def main():
        ...
        self.secondary(data)
        ...


def orchestrator():
    ...
    main_processor = MainClass()
    main_processor.main()
```

#### Simplicity:

#### Extensibility:
Best case: the new functionality properly belongs on the parent class, just like the old functionality.
```py
class ParentClass:

#   def secondary(self, data):
#       # Do stuff.

   def alternative(self, data):
       # Do different stuff.


class MainClass(ParentClass):

    def main():
        ...
        # self.secondary(data)
        self.alternative(data)
        ...


def orchestrator():
    ...
    main_processor = MainClass()
    main_processor.main()
```
* New method on parent class (base class).
* One-line change in child class, to call new method.
* No change in surrounding orchestrating code.

Worst case: The new functionality is realised to be not part of the parent class.  The whole abstraction is discovered to be wrong.  The inheritance hierarchy must be dismantled and rebuilt.
```py
# class ParentClass:
#
#   def secondary(self, data):
#       # Do stuff.


class BetterAbstractedParentClass:

   def secondary(self, data):
       # Do stuff.


# class MainClass(ParentClass):
class MainClass(BetterAbstractedParentClass):

    def main():
        ...
        self.secondary(data)
        ...


def orchestrator():
    ...
    main_processor = MainClass()
    main_processor.main()
```
* Whole new parent class required.
* Parent class of main class must be changed (one line change).
* Surrounding orchestrating code should not need to be changed.

However, in practice, this change will often be very difficult.  The original parent class may have many child classes.  So if the main class changes to a different parent, then the main class is no longer considered to be the same type of class as the other child classes.  This may have widespread ramifications for the design.

It seems that inheritance is a very brittle form of coupling.  The abstraction of the inheritance relationship needs to be exactly right, because it can be very difficult to change.  This implies that inheritance is not suitable for code that will developed in an agile, iterative fashion.

# Coupling Modules Into A Structure

### A Couple Of Structures: Tree And Linear

Connecting modules together produces a structure that can be considered to be a network of nodes and links (or 'edges').  (The mathematical field of _graph theory_ is the study of these structures and their properties.)

While there are an infinite number of possible structures, a couple of foundational 'platonic forms' will be familiar: trees and chains.  They are intuitive enough that diagrams will be sufficient reminders of their definitions.

#### Chain (Linear structure)

<svg width="500" height="40">
    <line x1="25" y1="20" x2="475" y2="20" stroke="red" stroke-width="8"/>
    <circle cx="25" cy="20" r="20" fill="blue"/>
    <circle cx="175" cy="20" r="20" fill="blue"/>
    <circle cx="325" cy="20" r="20" fill="blue"/>
    <circle cx="475" cy="20" r="20" fill="blue"/>    
</svg>


#### Tree

<svg width="500" height="340">
    <line x1="250" y1="20" x2="100" y2="170" stroke="red" stroke-width="8"/>
    <line x1="250" y1="20" x2="400" y2="170" stroke="red" stroke-width="8"/>
    <line x1="100" y1="170" x2="25" y2="325" stroke="red" stroke-width="8"/>
    <line x1="100" y1="170" x2="175" y2="325" stroke="red" stroke-width="8"/>
    <line x1="400" y1="170" x2="325" y2="325" stroke="red" stroke-width="8"/>
    <line x1="400" y1="170" x2="475" y2="325" stroke="red" stroke-width="8"/>
    <circle cx="250" cy="20" r="20" fill="blue"/>
    <circle cx="100" cy="170" r="20" fill="blue"/>
    <circle cx="400" cy="170" r="20" fill="blue"/>
    <circle cx="25" cy="320" r="20" fill="blue"/>
    <circle cx="175" cy="320" r="20" fill="blue"/>
    <circle cx="325" cy="320" r="20" fill="blue"/>
    <circle cx="475" cy="320" r="20" fill="blue"/>    
</svg>

# Make Execution Flow Obvious

Four paragraphs appearing at the beginning of the chapter _Distinguish Algorithm-like Code From Data-like Code_ apply here.  For convenience, we repeat them verbatim here:

Time is linear.  Time is just one damn thing after another.

Important corollary: The execution of a computer program is a _sequence_ of operations, one after the other.  We can say that program flow is _linear_.

Even more important corollary:  Reading is a linear process.  We read one element at a time, _incrementally_ building an understanding of the whole piece.

Thus, to answer "what does this code do?" is to understand the sequence of operations during the execution of the code.  Furthermore, our understanding of that sequence of operations is built by reading parts of the code, one after the other.

Therefore, a key principle for structuring code for readability is: **make execution flow obvious**.

Before exploring how to apply this principle, we shall first deal with the _exception_ - code that _does not_ have a meaningful execution order, which we have defined as 'data-like code'.

## Data-like Code Favours A Tree Structure

Data can be thought of as just a bunch of static variables.  However, the variables may be grouped in various ways, and the groups themselves may be further grouped into higher-order sets, forming a **hierarchy**.  Thus, a **tree-like** structure can be imposed onto the bunch of variables.  If the data is correctly abstracted in this way, it will make more logical sense, and be easier to understand.

Obviously, code whose main purpose is to represent data should be structured so as represent the abstract tree of variable groupings.  Then, accessing the data in the rest of the program will be as intuitive and logical as possible.

Consider an example of some data in JSON format.  The first example shows data in 'flat' format.
```json
{
    "student_id": 12345678,
    "name": "Joe Aloysius Bloggs",
    "email": "j.bloggs@gmail.com",
    "phone": 07412345678,
    "street_address": "21 Jump Street",
    "town": "Crapstone",
    "county": "Devon",
    "postcode": "PL20 7PJ",
    "bank": "Barclays",
    "account_name": "J A Bloggs",
    "sort_code": "12-34-56",
    "account_number": "87654321",
}
```
The second example shows the same data grouped into a sensible tree structure.
```json
{
    "student_id": 12345678,
    "name": "Joe Aloysius Bloggs",
    "contact_details": {
        "email": "j.bloggs@gmail.com",
        "phone": 07412345678,
        "postal_address": {
            "street_address": "21 Jump Street",
            "town": "Crapstone",
            "county": "Devon",
            "postcode": "PL20 7PJ",
        }
    },
    "bank_details": {
        "bank": "Barclays",
        "account_name": "J A Bloggs",
        "sort_code": "12-34-56",
        "account_number": "87654321",
    }
}
```
The second example with the tree structure is obviously _much_ easier to parse.

Suppose the JSON example above needs to be represented as a data structure in a computer program.  There are various ways of converting JSON into, for example, a composition of objects.  The details of that conversion are not important here - what is important is that the organised tree structure is preserved.  Assuming that details of reading and converting the JSON are abstracted away, then (Python) code that uses the data structure could look like this:
```py
student_json = read_student_json()
student = convert_json_to_student_object(student_json)

...

email = student.contact_details.email

...

postcode = student.contact_details.postal_address.postcode

```
As we can see, the tree structure is accessed in an intuitive way using the nested 'dot' syntax of object attributes.

The logical grouping and sub-grouping of all the data elements makes the data structure easy to understand and work with.  So favour tree-like structures for data-like code.

## A Fundamental Cause Of Badly-Structured Code

Now that we have seen how tree-like code structures can be a great idea, let us indulge in a rant about how tree-like structures can be a _terrible_ idea. 

Why do intelligent people write such obfuscated, tangled code?  Here is one reason:

They are organising code as if it were nothing more than a static bunch of text statements.  Of course, it _is_ a static bunch text statements, but crucially, it may be _more_ than that: there is another dimension to consider.  We'll come back to this point.

The intelligent but unwise programmer looks at code as a bunch of static text statements, and proceeds to 'organise' it.  The programmer abstracts out an underlying logical structure, and breaks the code into separate parts.  He or she carries on, further breaking each newly-created part into separate logical chunks.  The final result is a large number of separate pieces, all connected together in a **tree** structure.  The intelligent but unwise programmer is probably proud of this achievement, believing that he or she has cleverly followed the Separation Of Concerns Principle to the letter.  The code is now so beautifully _organised_.

Now, as we have seen, this is eminently appropriate as long as the code is **data-like**.

But most code in an application is algorithm-like. For algorithm-like code, this approach is completely and utterly wrong.  As we noted above, there is another dimension: time.  More specifically: execution order.

Algorithm-like code consists of a series of actions performed in a sequence.  To understand the code, one must understand the exact sequence of actions.  A linear type of structure obviously perfectly captures the sequence of actions.  On the other hand, a tree structure _obfuscates_ the sequence of actions.


## Algorithm-like Code Suits Linear Structures


As the preceding sections have made clear, linear-type code structures maximise the readability of algorithm-like code.  Let us consider a plan of attack for achieving well-structured code, using our skills of software abstraction to separate concerns.

Practical Advice:
1)  Most code follows the pattern handed down from the ancients: Take some data, do things to the data, put the data somewhere.
2)  Assume we are considering a non-trivial algorithm of this type, that takes up more than one screen of code to implement.
3)  Take the entire algorithm, and decide what the different *logical* elements are.  A logical element does *one thing*, it is a logically distinct operation.  This breakdown has nothing to do with the number of lines of code: Some operations can be done in one line of code, others in one thousand.  In other words, _separate concerns._
4) Create a separate function to do each logical element.  Because of the clean logical separation, it should be easy to give the function an accurate and complete self-documenting name.
5) Now the entry point, the algorithm in question, can be written as a 'main' or 'orchestrator' function containing a linear sequence of sub-functions.

Now, code is fractal: each logical element described above may itself be composed of distinct logical sub-elements.  The same principle applies at any level: for each element, write code that clearly reveals the flow of execution order.

Because of the fractal nature, we end up with code that has a nested structure, and is therefore tree-like in some sense.  However, the structure is _not_ a 'pure' tree - there is a critical additional property: The _linearity_ of each element means that an explicit _execution flow_ can be traced through the structure.

The diagram below illustrates the 'nested chain' structure.  The black arrows show the execution flow.

<div align="center">
<svg width="400" height="640">
    <defs>
        <marker id="arrowhead" markerWidth="10" markerHeight="8" 
         refX="8" refY="4" orient="auto">
            <polygon points="2 4, 0 8, 10 4, 0 0"/>
    </defs>
    <-- Main function -->
    <line x1="20" y1="20" x2="20" y2="620" stroke="red" stroke-width="8"/>
    <line x1="20" y1="220" x2="200" y2="120" stroke="red" stroke-width="8"/>
    <line x1="20" y1="220" x2="200" y2="320" stroke="red" stroke-width="8"/>
    <line x1="200" y1="120" x2="200" y2="320" stroke="red" stroke-width="8"/>
    <line x1="200" y1="253" x2="350" y2="187" stroke="red" stroke-width="8"/>
    <line x1="200" y1="253" x2="350" y2="320" stroke="red" stroke-width="8"/>
    <line x1="350" y1="187" x2="350" y2="320" stroke="red" stroke-width="8"/>
    <line x1="20" y1="520" x2="170" y2="453" stroke="red" stroke-width="8"/>
    <line x1="20" y1="520" x2="170" y2="587" stroke="red" stroke-width="8"/>
    <line x1="170" y1="453" x2="170" y2="587" stroke="red" stroke-width="8"/>
    <circle cx="20" cy="20" r="20" fill="blue"/>
    <circle cx="20" cy="120" r="20" fill="blue"/>
    <circle cx="20" cy="220" r="20" fill="blue"/>
    <circle cx="20" cy="320" r="20" fill="blue"/>
    <circle cx="20" cy="420" r="20" fill="blue"/>
    <circle cx="20" cy="520" r="20" fill="blue"/>
    <circle cx="20" cy="620" r="20" fill="blue"/>
    <-- Sub-function 1 -->
    <circle cx="200" cy="120" r="15" fill="blue"/>
    <circle cx="200" cy="187" r="15" fill="blue"/>
    <circle cx="200" cy="253" r="15" fill="blue"/>
    <circle cx="200" cy="320" r="15" fill="blue"/>
    <-- Sub-sub-function -->
    <circle cx="350" cy="187" r="15" fill="blue"/>
    <circle cx="350" cy="253" r="15" fill="blue"/>
    <circle cx="350" cy="320" r="15" fill="blue"/>
    <-- Sub-function 2 -->
    <circle cx="170" cy="453" r="15" fill="blue"/>
    <circle cx="170" cy="520" r="15" fill="blue"/>
    <circle cx="170" cy="587" r="15" fill="blue"/>
    <--   Flow arrows -->
    <line x1="50" y1="0" x2="50" y2="185" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="60" y1="182" x2="180" y2="115" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="225" y1="120" x2="225" y2="220" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="235" y1="212" x2="330" y2="172" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="375" y1="187" x2="375" y2="320" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="350" y1="345" x2="220" y2="280" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="220" y1="290" x2="220" y2="320" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="200" y1="345" x2="40" y2="250" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="50" y1="270" x2="50" y2="450" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <text x="37" y="475">Etc</text>
</svg>
</div>

An example sketch in Python would look something like:
```py
def main():
    config = read_config()
    data = load_data_from_file(config)
    transformed_data = operation_1(data)
    ...
    ...
    discombobulated_data = operation_4(transmogrified_data)
    ...


def operation_1(data):
    modified_data = sub_operation_1(data)
    ...
    mangled_data = sub_operation_3(altered_data)
    ...


def sub_operation_3(data):
    mutated_data = sub_sub_operation_1()
    ...


# Et cetera.
```

As noted in the section above _A Fundamental Cause Of Badly-Structured Code_, the point is _not_ to create a neatly-structured tree of nodes, with each node having minimal content, resulting in a very deep tree.  Therefore, resist the temptation to group the functions into higher-level functions with vague names like `transform()`.  This incredibly widespread plague of abstraction addiction is the *opposite* of writing readable code.

Furthermore, as noted in the chapter _Separate Input/Output From Computation_, Input dependencies such as reading a configuration file, reading environment variables from the operating system, loading a data file, _etc_, should happen at the **start** of the algorithm.  Making dependencies obvious is an important part of making code easy to understand quickly, so declare them up front. 


### The Daisy-Chain Anti-Pattern

Code with a 'daisy-chain' structure has a _linear_ structure, but lacks a proper 'main' or 'orchestrator' function.  Code consists of a chain of function calls, where each function calls the next function in the sequence, instead of returning back up to an orchestrator.  There are two main flaws of this structure:

1. With no 'main' or orchestrator function, the overall structure of the algorithm cannot be seen anywhere.  One must read all the functions in turn to build a mental picture of the key steps in the algorithm.
2. The entry point will be the first function in the sequence.  Since it will have a single clear concern, it should have a simple descriptive name such as `read_data_file()`.  However, its final act is to call the next function in the sequence, thus ultimately executing the entire program.  Executing the entire program is the _mother_ of all side-effects for a simple function!

So don't do this.  Instead, use the (nested) linear structures with orchestrators described in the previous section.

The example sketch above structured in this anti-pattern would look something like this:
```py
def read_config():
    ...
    load_data_from_file(config)


def load_data_from_file(config):
    ...
    operation_1(data)


def operation_1(data):
    ...
    operation_2(data):


def operation_2(data):
    ...
    operation_3(data)
```

## Summary

The structure of code should reflect its purpose.  Is the purpose of a module of code to store data or is it to do some computation?

Note that a data-like code component may still have algorithm-like code within it, for example, non-trivial accessor methods on a complex data structure.  Within those accessor methods, the advice for algorithm-like code applies (favour linear 'nested chain' structures).

> **Code should look like what it is.  Code should look like what it does.**


# Data Flow Should Follow Execution Flow

Let us start with an analogy...

> Imagine you are on a police surveillance team, watching suspicious comings-and-goings on Functional Street.  You walk past Larry's Barber Shop, and see that it is empty except for Larry himself.  A little while later, from a distant observation point, you observe three shady individuals leave Bada Bing club and enter Larry's Barber shop.  A police sniper contacts you by radio, and asks how many people are in Larry's. You answer "Four".

> Now, on a similar assignment, you are conducting surveillance on Object-Oriented Avenue.  After chatting to Mr Sharp who is alone in his shop, you retire across the street to discreetly observe.  You see three dodgy characters leave The Red Lion pub and enter Sharp's Bait and Tackle.  Anticipating the question, you think about how many people are in Sharp's.  What is the correct answer?  Four?  Nope.  There are seven.  What?  _People came in the BACK DOOR_.  Five minutes later, your radio crackles to life with the question "How many people are in Sharp's?"  How many indeed?  The correct answer is: zero.  What?  _They all left through the back door_.

This story is analogous to reading code where the data flow does not follow the control flow.  The control flow (or execution flow) is what you are reading, line-by-line, as you try to understand what it does.  Data flow describes the movement of data between different components.  Suppose you are reading the code, and see that `function_A()` is executed, followed by `function_B()`.  Further suppose that just by reading the code in front of you, you see that data generated by `function_A()` is passed as input into `function_B()`.  Then we can say that Data Flow is following Control Flow.

Interestingly, Data flow is something you don't think about *unless* it deviates from the execution flow.  How might it do that?  By the use of evil *global variables*.

### Evil Global Variables

Most CPUs work by executing machine code instructions and storing values in registers, which are later read by other instructions.  When the first higher-level languages were developed, they tended to follow this model of doing some operation, storing the output value, then having subsequent operations read the value from its memory store.  It was some time before experience with larger-scale software programs showed the dangers of this approach.

A concrete example of the use of global variables in Python:
```py
evil_global_variable = 0

def main():
    operation_1()

    if evil_global_variable == 1:
        operation_2()
    else:
        operation_3()


def operation_1():
    ...
    evil_global_variable = peculiar_computation()
    ...


def operation_2():
    ...
    # Lots of computation that does not use evil_global_variable.
    ...


def operation_3():
    ...
    result = 3.1415927 * r^2 * evil_global_variable
    ... 
```
The opacity and obfuscation are obvious in the example above.  Simply by reading the code in `main()`, one cannot know that `operation_1()` _sets_ `evil_global_variable`, while `operation_2()` does not use `evil_global_variable` at all, and `operation_3()` _depends on_ `evil_global_variable`.

Thus, global variables force the reader to make much more mental effort to understand the code:  You have to read every single damn line to see where global variables are being set, and remember that fact as you read on.  Then much later, when you encounter code that reads that variable, you have to remember the state of that variable.  So you have to keep a parallel thread in your mind.  You are reading code - that is one mental thread - but now you need another mental thread to track the flow of data between functions.

The effort of reading _all_ the code might be reasonable for a small code base, but this becomes a huge time cost as the code base gets bigger.  And the cognitive task of maintaining a mental thread of the global variable value becomes simply unfeasible for large enough code bases.  This will inevitably lead to bugs.  Consider this scenario: `function_A()` dumps a result to a global variable.  Some time later, `function_B()` reads that variable as an input.  But surprise!  That new bit of code your colleague wrote yesterday alters the global variable before `funtion_B()` access it.  And that is why you are debugging today...

So don't do this.  Make data follow the control flow.  Pass necessary data in, so that you can see it right there as you read the code that uses it.  Here is the example code fixed:

```py
def main():
    local_variable = operation_1()

    if local_variable == 1:
        operation_2()
    else:
        operation_3(local_variable)


def operation_1():
    ...
    local_variable = peculiar_computation()
    ...
    return local_variable


def operation_2():
    ...
    # Lots of computation that does not use evil_global_variable.
    ...


def operation_3(local_variable):
    ...
    result = 3.1415927 * r^2 * local_variable
    ... 
```


### An Object-Oriented Trap

The code in the example above that uses global variables is terrible!!!  So let us 'fix' it by applying the panacea of object-oriented programming!!!
```py
class AnAllTooTypicalClass:

    def __init__():

        self.perfectly_innocent_class_variable = 0

    def main():
        self.operation_1()

        if self.perfectly_innocent_class_variable == 1:
            self.operation_2()
        else:
            self.operation_3()

    def operation_1():
        ...
        self.perfectly_innocent_class_variable = peculiar_computation()
        ...

    def operation_2():
        ...
        # Lots of computation that does not use perfectly_innocent_class_variable.
        ...

    def operation_3():
        ...
        result = 3.1415927 * r^2 * self.perfectly_innocent_class_variable
        ... 
```
Much better!!!  Object-oriented design saves the day!!!  The evil global variable has been _encapsulated_, and the problems have been fixed.  Right?

Sadly, no.

A careful look will reveal that the problematic structure is _exactly the same_, it has just been transported down a level from the file level to the class level.  Adding an extra layer of abstraction - the class - has not changed the relationship between the troublesome variable and the functions that access it.  (Note that in this example, the extra layer of abstraction adds no benefit, and has therefore made the code worse.)

We have uncovered a serious 'foot gun' of object-oriented design.  Various claims about the desirability of 'data encapsulation' _etc_ obscure the fact that object-oriented design positively encourages the use of what are effectively global variables.  Adding an extra layer of abstraction and relabelling them to 'object attributes' does not eliminate the problems they cause.

Now, the problems with the object-oriented example code above _could_ be fixed by eliminating the object variable, and passing data directly into methods that use it.  However, we should look at the bigger picture and consider the issue from a higher level of abstraction, which we'll consider next.

#### When To Use Objects

Objects are very good at capturing _state_.  They are excellent for carrying around variables and methods (functions) that access those variables, though care must be taken to ensure that the state is always forced to be consistent.  This code construction is so useful that even strict functional languages such as Haskell have it.

Problems arise when objects are used as containers for _algorithm-like_ code.  As the example above shows, a common anti-pattern is to have a class that carries out a complex algorithm using what are effectively global variables.

The structure of an object is inherently tree-like, and as the section _Make Execution Flow Obvious_ argued, algorithm-like code suits linear-type structures, while data-like code suits tree-like structures.

A _possible_ use case for an object that carries out complex algorithms is as a _context_ for the computations, in which the object attributes are all _immutable_, so that the object does not have global variables but rather global _constants_.  Then the functions can easily access the global constants.  However, since there are no encapsulated variables, some would argue that this violates principles of object-oriented design, and a class should not be used in this instance.  So we do not advise doing this -  we merely mention this _theoretical_ use case for completeness.

In general, just separate the concerns of algorithm-like code and data-like code, and follow these rules of thumb:

> Make objects **small**, and chiefly concerned about **carrying state**.  Use as few objects as possible, but no fewer - separate the different kinds of state into separate objects.

The above advice is a general corollary of the Golden Rule: Separation Of Concerns.


# Interfaces: The Glue That Connects

An **interface** to a code module is the point of entry.  Examples include:
* A function call.  The interface is defined by the function name and signature (arguments passed in).
* Class instantiation, and the suite of public methods on the object.
* Internet requests via the `http` protocol.

An Application Programming Interface (API) is any interface that a programmer could use, by learning the protocol, and writing correct code for it.  In practice, the words 'API' and 'interface' are generally used interchangeably.

An interface may be private or public.  Somewhat different guidelines apply between private and public interfaces.

#### Private Interfaces

Private interfaces can be modified without external consequence.  Furthermore, private interfaces _should_ be modified as the program iterates towards a sound structure engineered for readability.  The _ideal_ interface should emerge organically as the program is developed.

#### Public Interfaces

Any interface that an external party uses is _public_.  Therefore, modifying the interface will affect the external party.  If the external party is just some engineers on the other side of the office, then this can be coordinated.  However, if the external party could be any random user on the internet, then more care is required.

In general, a public interface should be **versioned**, so that if it is changed, the change is explicitly advertised.

A public interface needs _much_ more care in its design than a private interface, because it is much harder to change.

### API Design

#### Multi-Granular

Especially for a non-trival public API, the interface should have **different levels of granularity**.  This means:

1. **Atomic operations** should be defined and exposed.  These are the lowest-level building blocks of API operations.  This is the lowest level of granularity.  The atomic operations should form a **complete set**, so that any possible action with the API can be achieved by a sequence of atomic operations.

2. **Routine operations** should be possible with a single simple call.  That is, the most common uses of the API should be _trivial_ to achieve.  Internally, each routine operation should use atomic operations, so that by definition, a routine operation call is equivalent to a sequence of atomic operation calls.

3. Further operations should be defined _very sparingly_.  Outside of the full set of atomic operations, and operations for the commonest use cases, it is wise to be very reluctant to add any more.  Further operations add confusing bloat to the API, and are a maintenance burden, both of which are costs that are probably greater than the value of adding an API call for some obscure operation.

#### Consider Using Specification Data Objects

Suppose you are developing a function that is turning out to have rather a lot of parameters.  The function call is becoming unwieldy.  Furthermore, many of those parameters must be further passed down into sub-functions, that are themselves suffering a bloated signature.

Now, this _may_ be a sign of a bad abstraction - is the function trying to do much?  Should it be broken into separate concerns?  However, let us assume that it is indeed a good abstraction, and the entry point really does require that many parameters, due to the nature of the domain problem.

One solution is to modify the function signature to accept a single rich data object, instead of a multitude of low-level parameters.  The 'parameter space' is thought of as a separate concern that can be abstracted out into a data object.  Generally, this abstraction will represent a _specification_ for the algorithm that the function carries out.  This spec object can be easily passed down into sub-functions, which tends to significantly tidy up code.

One possible benefit of this approach is that the _effective_ signature of the function can be changed _without_ actually changing the function signature, by simply modifying the structure of the specification data object.  Of course, changing the spec object may cause its own problems: strictly speaking, we are still changing the API.  But the hope is that this form of change will be easier than changing the function call itself.

This advice on API design is an example of the application of previous advice to separate state into its own object, since objects are perfectly suited for data-like code.


# Miscellaneous Advice

Some advice on low-level code constructions that nevertheless have a big impact on code readability.

##  Name Things Clearly

Everything in your code should have a name that is precise, descriptive, and at the appropriate level of abstraction.  Then your code can be said to be _self-documenting_.  If the reader trusts that all names have been chosen with care, then the reader can understand the code much more quickly because the names describe what each piece is and does.  Self-documenting code also needs fewer comments to explain the code.

However, naming things is _hard_.  The skill of naming things well takes a long time to develop.  Perhaps this skill is one signifier of a 'senior engineer'.  Here are some guidelines to consider when trying to find a suitable name.

For clarity, consider a simple floating-point number variable that needs a self-documenting name.  The variable name could:
1. Describe what it **is**, in the sense of 'how it was constructed'.  For example, a variable computed from the sum some financial transactions could be called `sum_of_transactions`.
2. Describe what it will be **used for**.  For example, if the variable is fed into a function that ultimately generates a financial statement, then an appropriate name could be `sum_for_statement_generator`.
3. Describe what is **is**, in the sense of 'what it means, in the context of the problem domain'.  For example, the variable _actually_ represents net profit, then an obvious candidate name would be `net_profit`.

Options 1 and 2 are the easiest to work with.  Either one would likely add _considerably_ more value than a vague variable name such as `val`.

However, Option 3 is likely to be the most valuable.  Describing the _meaning_ of a variable, _why it matters_, will generally give the most insight into what the code as a whole is supposed to achieve.  But this is also generally the most difficult option to implement: It requires a proper understanding of the problem domain, and the skill at seeing the correct level of abstraction to describe this small part of the domain.

Naming things is _hard_.  But the payoff of good, self-documenting variable names is huge, so persevere in finding them.


## Code Hygiene

The phrase 'code hygiene' is sometimes used to refer to the practice of cleaning up temporary files and other sundry mess resulting from software development, and keeping necessary configuration files _etc_ in a tidy state.  The idea is to keep your engineering workspace in a state that minimises confusion.  A few hints follow.

Don't call a file `data.txt`.  Call it what it is.  Spend 60 seconds thinking of a great name.  This will save _many minutes_ in the future.  So call it something like `user_accounts_2023-01-21.txt`

Delete temporary files as soon as you can.  They are supposed to be _temporary_.

A common problem is that you can't delete a temporary file immediately, because you may need it again in a few hours or days.  So try this trick:  Put a deletion date in the file name.

Eg. `user_accounts_2023-01-21_DELETE_AFTER_2023-02-01.txt`

Then, in six months time, when you stumble across this long-dead file again, you won't have to spend time investigating whether or not it is safe to delete.


---
Work In Progress below this line.

## Use Inclusive-Exclusive Ranges

Though it appears to lack symmetry, using closed/open ranges makes the arithmetic much simpler, and gets rid of loads of code to handle edge cases.

There's a reason the Python range() function uses this convention: `range(3, 6) = [3, 4, 5]`.

# Thinking Like An Engineer

## Be Explicit

Crush Ambiguity.

A callback to the art of abstraction first encountered at the beginning of the book.  'Be Explicit' is another rule for creating good abstractions at the right level.

## Single Source Of Truth


## Format Code Perfectly At All Times

Keep code formatting perfect at all times.  _Don't_ say to yourself "I'll come back and fix the formatting later."  Write your code in the same way that proper chefs practise 'clean as you go' in a commercial kitchen.  This discipline helps instil both the attention to detail and sensitivity to structure that characterise a good engineering mind.

# Case Studies?: Polymorphism?

The classic example with `square.area()` and `circle.area()` illustrating the power of method polymorphism.
