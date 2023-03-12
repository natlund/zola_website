+++
title = "Readability"
date = 2022-12-19
weight = 10

[extra]
next_page = "elementary_code_structures.md"
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
