+++
title = "Readable Code (Archived)"
date = 2022-03-14
weight = 20
+++


_A document written early in my Quant Software Developer career.  At the time of writing, I had worked with a terrible, malformed object-oriented code base every day for approximately a year, and spent many productive hours discussing it with a colleague.  The ideas herein are sound, but have been expanded and improved in other essays.  This essay is 'archived', but is an interesting snapshot of my understanding at that time._


Let's start with a very common everyday challenge that a developer faces:  You are working with an unfamiliar code base, and you have to use some function or object.  The immediate question is:

"What the hell does this do?"

Perhaps the function is part of an API; in any case it is the entry point into the code, and also the entry point of our discussion here.

The question "what the heck does this do?" gives us a good basis from which to define readability.

**Definition:  READABILITY:**  The (inverse) time taken to satisfactorily answer the question "what does this do?"  The most readable code takes the least amount of time to understand.  Unreadable code takes a long time to understand.

Obviously, we need to be comparing apples with apples:  We are considering different ways of coding the *same functionality*.  From the same entry point, there are an infinite number of different ways of implementing the same functionality.  Our concern is ranking those different ways by how long they take to understand - to rank them by readability.

Equally obviously, there is a subjective element.  Different developers are accustomed to different coding styles.  Developers vary enormously in their experience and exposure to code.  People will insist that things are "a matter of taste."  So, we are interested in principles of readability that are universal, in the sense that most reasonable people will agree.  We cannot account for the absurd opinions of highly non-neuro-typical outliers, so we won't bother.  What we seek are reasonable, defensible principles that are helpful in the vast majority of situations.

What follows are three interlinked principles that go a long way towards making code readable.


## Principle of Obvious Execution Flow

Time is linear.  Time is just one damn thing after another.

Important Corollary: The execution of a program is a *sequence* of operations, one after the other.  We can say that program flow is *linear*.

Even more important corollary:  Reading is a linear process.  We read one element at a time, *incrementally* building an understanding of the whole piece.

Now, to answer "what does this code do?" is to understand the sequence of operations during its execution.  Furthermore, our understanding of that sequence of operations is built by reading parts of the code, one after the other.

Claim: Since execution of code is a linear sequence of operations, and reading of code is a linear sequence of operations, code should structured to as much as possible reveal that linear sequence.

Observation:  Very often, code is written in a *tree-like* structure that *hides* the flow of execution.  Even worse, the deeply-nested tree must be read by mentally following a tree-parsing algorithm that requires the reader to maintain a mental 'stack' to assemble the elements into the execution order.

Now, *data* is usually naturally tree-like.  There is typically an obvious hierarchy of categories.  In fact, non-trivial data structures (such as a json file) *need* to have a sensible tree structure, otherwise they become unwieldy.

Trees have tremendous power to bring order to a programmer's file system, home directory, json files, music collection, etc.  And so programmers have a tendency to organise their *code* into trees.  The assumption is that a tree hierarchy makes code better organized - things are in neat logical categories, and you always know where to find things.  Unfortunately, this is wrong. Data is *static*.  But code has *another dimension:* execution order.  Execution is the *whole point* of code.  Execution order completely over-rides any considerations regarding the hierarchy of logical categories in the code.

Principle: Structure code such that the execution order is as clear as possible.  Favour linear constructions.  Tree-like structures usually obfuscate.

Practical Advice:
1)  Most code follows the pattern handed down from the ancients: Take some data, do things to the data, put the data somewhere.
2)  Assume we are considering a non-trivial algorithm of this type, that takes up more than one screen of code to implement.
3)  Take the entire algorithm, and decide what the different *logical* elements are.  A logical element does *one thing*, it is a logically distinct operation.  This breakdown has nothing to do with the number of lines of code: Some operations can be done in one line of code, others in one thousand.
4) Create a separate function to do each logical element.  Because of the clean logical separation, it should be easy to give the function an accurate and complete self-documenting name.
5) Now the entry point, the algorithm in question, can be written as a linear sequence of functions.

Resist the temptation to group the functions into higher-level functions with vague names like `transform()`.  This incredibly widespread plague of abstraction addiction is the *opposite* of writing readable code.

Now, code is fractal: each logical element described above may itself be composed of distinct logical sub-elements.  The same principle applies: write code that clearly reveals the flow of execution order.  Because of the fractal nature, we end up with a tree.  This principle is not that "trees are bad".  The point is to clarify *why* you have created a tree.  A bad tree is a thoughtlessly-constructed hierarchy of vague abstractions that obfuscates the flow.  A good tree is the natural and healthy consequence of describing 'what it does' at the appropriate level of detail for a given level of abstraction.


## Principle that Data Flow should follow Control Flow

Imagine you are on a police surveillance team, watching suspicious comings-and-goings on Functional Street.  You observe three shady individuals leave Bada Bing club and enter Larry's Barber shop.  A police sniper contacts you by radio, and asks how many people are in Larry's. You answer "At least three."

Now, on a similar assignment, you are conducting surveillance on Object-Oriented Avenue.  You observe three dodgy characters leave The Red Lion pub and enter Sharp's Bait and Tackle.  Anticipating the question, you think about how many people are in Sharp's.  What is the correct answer?  Three?  Nope.  There are seventeen.  What?  *People came in the BACK DOOR*.  Five minutes later, your radio crackles to life with the question "How many people are in Sharp's?"  How many indeed?  The correct answer is: zero.  What?  *They all left through the back door*.

This story is analogous to reading code where the data flow does not follow the control flow.  The control flow is what you are reading, line-by-line, as you try to understand what it does.  Data flow describes the movement of data between different components.  Suppose you are reading the code, and see that Function A is executed, followed by Function B.  Further suppose that just by reading the code in front of you, you see that data generated by Function A is passed as input into Function B.  Then we can say that Data Flow is following Control Flow.

Interestingly, Data flow is something you don't think about *unless* it deviates from the control flow.  How might it do that?  By the use of evil *global variables*.

Global variables are dangerous as hell, everyone knows that.  But if you use them *inside an Object*, and call them 'attributes', then suddenly nobody notices them.

The most egregious use of ~global~ object variables is for passing data between functions.  Method A dumps a result to an object attribute.  Some time later, Method B reads that attribute as input.  But surprise! That new bit of code you wrote yesterday alters the attribute before Method B has used it.  And that is why you are debugging today...

Message passing by global variables makes code incredibly hard to read.  You have to read every single damn line to see where global variables are being set, and remember that fact as you read on.  Then much later, when you encounter code that reads that variable, you have to remember the state of that variable.  So you have to keep a parallel thread in your mind.  You are reading code - that is one mental thread - but now you need another mental thread to track the flow of data between functions.

Don't do this.  Make data follow the control flow.  Pass necessary data in, so that you can see it right there as you read the code that uses it.

Sardonic observation:  In this respect, OO positively *encourages* bad coding.

Observation:  There is probably a good reason why programmers are so strangely accepting of message passing by global variables:  this is how you program in assembly language, and Fortran and C remain close in spirit to that style.


## Principle of Explicit Dependencies

When you start at a code entry point and ask "What does this do?", there are two implicit sub-questions:
1) What does this depend on?  What does it need to work?
2) What depends on this?  What will be affected by this thing running?

There are two main kinds of dependencies: imports and Input/Output (IO).  Imports are typically not a problem: they are declared in one place at the top of the file.  (There is an argument for preferring *dependency injection* over importing, but that is beyond the scope of the current article.)  IO includes: reads and writes to a database, reading configuration from a YAML file, checking the time, and possibly reading from object or class attributes (global variables).  Output may be considered to have a *side effect*: other program entities are altered, or their behaviour is changed due to the side effect.

If our code entry point does IO, we should make that dependency explicit at the top level of the code.  DO NOT hide it inside a nested sub-function.  Try to put it in an explicitly-named top-level function, like `get_customer_info_from_database()`.

An excellent rule of thumb is do Inputs at the beginning, Outputs at the end, and in the middle, use *pure functions* as much as possible.  In rare cases, code might be more readable if some IO occurs in the middle somewhere.

A pure function takes an input, returns an output, and does nothing else.  It does not read from the database, check system time, or write to anything (with the possible pragmatic exception of writing logs)  The same input always returns the same output.  It does not depend on the day of the week, config in a YAML file that may change, or the phase of the moon.

(Incidentally, pure functions automatically force data flow to follow control flow - it can't happen any other way.)

The idea is that someone reading the function can quickly see the dependencies.  "Oh, this function needs a valid yaml config file to exist."

In general, IO and side effects should only occur at the Beginning or End.  Pure functions in the middle.


## Summary:

**Principle:** Make execution flow clear.  Make control flow explicit.

**Principle:** Make Data Flow follow control flow.

**Principle:** Make dependencies explicit.  Two ways: pure functions when possible, and do IO at beginning and end only.
