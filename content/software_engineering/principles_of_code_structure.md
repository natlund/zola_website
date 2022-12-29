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

2. You Ain't Gonna Need It (YAGNI).  Don't solve tomorrow's problems.  Premature Optimisation is the root of all evil (_Knuth_ 1968). Because:
    * What is the best time to design a system for extensibility?  Answer: at the time you actually have to extend it.  Only at that point do you have the maximum possible information on the problem.   At any earlier time, you have less information, so will likely make worse engineering decisions.

4. Code that is easy to extend tends to have a very modular stucture, with minimal coupling.  Happily, those are properties of highly readable code also.  Thus, code that highly readable tends to be highly extensible.

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

The value of such set hierarchies is that they underpin logical inference.  A classic illustration is the logical syllogisms formalised in Ancient Greece: "All humans are mortal.  Socrates is a human.  Therefore, Socrates is mortal."  Various other logical rules have been formalised.

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
  * For example, the quark subatomic particle started out as a purely mathematical abstraction that simplified and clarified the theory of subatomic particles.  But much later, high-energy physics experiments confirmed the physical existence of quarks.

But if our abstractions cannot be tested with the rigour of science, then how do we decide if they are 'good' or not?

The answer to this question is deep, and beyond the scope of this essay.  Only some rough guidelines can be suggested:
  * A good abstraction **simplifies** our understanding of the situation.
  * A good abstraction **unifies** various disparate elements, that were previously seen as having no relation.
  * A good abstraction will tend to be **generally applicable**, to a wider problem space beyond the current problem.  It may have __predictive power__.
  * A good set (or hierarchy )of abstractions will be **internally consistent**.  There will be no contradictions.

Thus, abstract reasoning is actually very risky, in the following sense: It can be done very badly, leading to a false understanding of the universe, and that false understanding may persist for a very long time, because of the difficulty of testing it.  Enormous amounts of time and energy may be wasted on building castles in the air, discussing how many angels may dance on the head of a pin.

Primitive people don't suffer much from this problem, because errors in concrete thinking are usually immediately visible.  "Trust me, there are no bears in this cave!"  _Chomp_.  But it doesn't take much additional cultural sophistication to suffer badly from it.  "We need to throw a virgin into the volcano to prevent it from erupting".  _"Aaaaargh_".  Silence.  "See, it's working."

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

The 'complexity' of a computer program is difficult to define precisely, but for our purposes, it suffices to employ common-sense notions along the lines of 'complexity = amount of stuff, and amount of connections between stuff'.  More complexity is obviously harder to understand.  A key focus of good software engineering is managing complexity: disentangling it, and minimising it.

Complexity can be broken into three different types:

#### Inherent Complexity

Inherent complexity is the complexity of the actual domain problem itself.  It may be the complexity of a mathematical algorithm, or the complexity of some business logic, or the complexity of managing a long-term interaction with a user.

Inherent complexity cannot be reduced, because it is inherent to the domain problem itself.

#### Collateral Complexity

Collateral complexity is the complexity in the details of the solution to the domain problem, that is not inherent to the problem.  This is best explained with an example:

Suppose the domain problem requires saving some data to a database.  The action 'save data to database' is considered part of the _inherent complexity_ of the problem, because it is a critical step in the algorithm.  But the _details_ on how to connect to the database, where the passwords are stored, the exact protocol for calling a Postgres database, _et cetera_, are considered to be only _collateral_ complexity, because these low-level details do not fundamentally matter to the solution.  This collateral complexity is essential to solve the domain problem, but it is not _inherent_, because the details could change quite drastically (for example, by changing to a different database) without affecting the operation of the solution.

#### Accidental Complexity

Accidental complexity is any complexity in the design that is _not_ essential to solve the domain problem.  The problem has an inherent complexity, and there is the collateral complexity of the low-level details _required_ to solve the problem, and any remaining complexity is essentially due to _bad design_.

Classic examples include: poor use of Object Oriented design, unstructured spaghetti code, having the wrong abstractions, confusing or obscure variable names, 'clever' code that is more generalised than it needs to be, _et cetera, et cetera, ad nauseum_.

The point about accidental complexity is that is _can_ and _should_ be eliminated.  In this sense, it is completely different from collateral complexity, which _cannot_ be eliminated.

#### Notes

Separating inherent complexity from collateral complexity is a good example of the art of abstraction at work, and one of the first abstractions that novice programmers naturally tend to start doing.  Pulling the boring details of a database connection into a _separate function_ is an excellent and easy first step towards a better program structure.  Several lines of code are recognised to be all contributing to the same _abstract_ activity - 'save to database' - and are not part of any other concern.  Therefore, this Concern is separated out into its own function.  Engineers would often describe this with language like "abstracting out the database connection."

A corollary is that the function call `save_to_database()` is at a higher level of abstraction, and that level of abstraction is inherent to the problem solution.  An _essential_ step of the solution algorithm has now been made explicit with a self-documenting function name.  The code is now easier to understand; it is more readable.

In summary:
1. Separate Inherent Complexity from Collateral Complexity.
2. Eliminate Accidental Complexity.  Or at least understand the trade-offs.


# Separation Of Functions From State

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
    * In non-deterministic ways, for example, due to user input.
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


#### Warning:  Don't Add Complexity Via Too Little State

It is sometimes possible to completely eliminate state by using constructions found in functional programming languages.  A classic example is recursion.  A `for` loop may be eliminated by using a function that recursively calls itself.

But this is a bad idea:  Recursion is _considerably harder_ to understand than a simple `for` loop with state.  Our goal is not to be clever, but to write readable, maintainable code.  So don't do this sort of thing.  The goal is not to eliminate state at all costs, but to reduce the use of state down to the point where it maximises readability.  A little bit of easy-to-understand state is vastly better than a confusingly 'clever' stateless solution borrowed from functional programming.


# Separate Input/Output From Computation

A lot of computer code follows the pattern handed down to us from the ancients:
1. Get some data from somewhere.
2. Do some computations from the data to produce new data.  Equivalently, _transform_ the data.
3. Put the new data somewhere.

Separate the code that does Input or Output into its own modules.  Do _not_ make an I/O call in the middle of some code that is doing a computation.

Rules of thumb for readable code:
1. Try to put the calls to the Input module at the beginning of the program.
2. Try storing the input data in some kind of State module, for later use.
3. Try to put he calls to the Output module at the end of the program.

Input and Output are major dependencies of the program.  For example, a program may depend on the existence of a config file as input.  Now suppose the config variables are not needed until half way through the program.  An 'efficient' programmer might delay reading the config file until the point at which it is needed.  However, it is better to read the config file at the very beginning of the program, because:
1. It makes the dependency on the existence of the config file immediately explicit to the reader.
2. If the file is missing, the program will error immediately, instead of wasting time on a computation that will ultimately fail.

Make dependencies explicit.  (See chapters on Coupling.)  Fail early.  Make sure you have everything that you need before starting the job.


# Separate Business Logic From Mechanical Work

Business logic is the _whole point_ of software.  Software is engineered to solve business problems.

Therefore, in your code, _highlight_ the business logic.  Try to elevate it to its own module so that the business logic is _obvious_.  This also tends to make it easier to modify the business logic.

Code is often read for debugging purposes, or to answer a question about system behaviour that is not documented.  These are issues of business logic: "What is the system supposed to do, and is it actually doing it?"  Therefore, make life easy for everybody by making business logic extremely explicit, sitting by itself in an easy-to-find place.  Keep it _separate_ from low-level mechanical details about _how_ the system implements that business logic.

Deciding what counts as business logic may not always be easy.  But try to keep this separation in mind when designing the system.  This abstraction is one that _matters_.


# Collate The Concern Of Logical Branching

If your code requires a logical branch, try to do it only once.  Your code will be much cleaner and easier to read.

Making the _same_ logical branch (i.e. exactly the same logical conditions) in _multiple_ places should be considered an anti-pattern, or at least a code smell.  The resulting code is always cluttered and messy.  Try to refactor it to have only one occurrence of the logical branch.


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

The value of assessing Simplicity is obvious, since we value readability above all else.

The value of assessing 'Swappability' needs a little more justification.  We may **know** that the code will need to be modified in the future.  In that case, we want to choose methods of connection that give the best compromise between readability and extensibility (ideally, maximise both).  Furthermore, by explicitly analysing the extensibility of a method of coupling, we can pre-empt a lot of vague, misguided bleating about 'reusable code' that OO tossers are prone to emit.  Those wankers often claim that some stupid OO solution is better, when actual analysis of the solution often reveals that it is not.  These pricks just parrot OO dogma without actually examining it in the real world.

Other justifications for making connections 'Swappable': 1) Don't create tomorrow's problems.  2) More easily swappable means more loosely coupled, which in turn tends to correlate with cleaner separation of concerns.

Hmmm.  Maybe this section needs some justification in the first chapter on Readability, at the bit where I rant about extensibility.

### Types Of Connections

Some types of connection, in approximate order of simplicity.

1. Function call.
2. Function call of injected function.
3. Method call on class.
4. Method call on injected object.
5. Object instantiation, then method call on object.
6. Inheritance.  Method call on parent class.


# Coupling Modules Into A Structure

### A Couple Of Structures: Tree And Linear

### A Couple Of Types Of Code: Algorithm-like And Data-like


# Principles Of Coupling Modules Into A Structure:

1. Make dependencies explicit, by putting them at the top, or entry point, of the program.
2. Code should look like what it does.  Code should look like what it does.  Data-like or algorithm-like.
3. Make execution flow obvious.
4. Data flow should follow execution flow.

# Case Study: Polymorphism

The classic example with `square.area()` and `circle.area()` illustrating the power of method polymorphism.

