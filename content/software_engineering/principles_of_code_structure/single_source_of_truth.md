+++
title = "Single Source Of Truth"
date = 2025-04-23
weight = 55
+++

# Single Source Of Truth


## Collation Of Concerns

In the previous chapter [_Separation Of Concerns_](@/software_engineering/principles_of_code_structure/separation_of_concerns.md), we established the value of a single module of code only dealing with a single concern.

The complement to that is to pull all the code that deals with the same concern into a single module of code.  In other words, _collate_ all the code that deals with a single concern, and put it in a single module.

This improves readability.  For a single given concern, the corresponding code only needs to be read _once_.  The reader will not find themselves wondering "Wait, is this code essentially the same as that other block of code I read earlier?"

A single code element that captures a single concern and is used in more than one place is known as the 'Single Source Of Truth'.  The name highlights how the structure supports the _correctness_ of the code.  Robustness is improved, not just readability, as we'll illustrate in the following example.

## Single Source Of Truth

Consider a piece of code dealing with some important concern.  It need not be very big - for example, it could be a single configuration value, perhaps just a boolean flag.  Or it could be something bigger, such as a function that does some mathematical calculation.

Now consider the situation where the code is _duplicated_ - there are two (or more) functionally identically pieces of code.  Now let's imagine that at some point in time, the two copies _diverge_ so that they are no longer identical.  This can easily happen if, for example, one copy was updated, but the other was forgotten.  Finally, let's assume that the divergence is a _bug_, the program as a whole is no longer correct.

The obvious solution is to _not_ have duplicates, but rather to have a single piece of code that deals with the critical concern - the Single Source Of Truth.  That way, when the concern changes in any way, code needs to be modified in only one place, and overall program consistency is always guaranteed.

## Similar Sources Of Truth - Do Not Collate

Now consider the _superficially_ similar situation: There are two (or more) functionally identical pieces of code.  But now, the two pieces of code have different _purposes_ or _meanings_; they are semantically different.  In other words, from a certain point of view, the two apparently-identical pieces of code _do not deal with the same concern_.

This may seem very subtle and confusing - how can we tell if two apparently-identical pieces of code deal with the same concern?  The litmus test is this:  Could the two pieces ever evolve in different ways so that they are no longer identical?  As the code base changes over time, could it ever be correct for the two pieces to be no longer identical?  If the answer is yes, then in the most important sense, the two pieces of code **do not** deal with the same concern.  Therefore, they should **not** be collated into a Single Source Of Truth.

Because this point is quite subtle, and the misleading advice "Don't Repeat Yourself (DRY)" is often mindlessly followed, we often see this anti-pattern of superficially identical code fragments being collated into a Single Source Of (More-Than-One)Truth.  One sign of this that the code module for the Single Source Of Truth has acquired a _parameter_ or two to 'handle the different cases'.

A single parameterised function is generally _worse_ than two separate but simple functions, even with considerable code repetition.  A parameterised function is much more onerous to test, and much harder to read and reason about.  Getting the parameter wrong for the use case is a potential bug.  So just use two simple separate functions.  Fight the demon of Abstraction Addiction!

## DRY Done Right

The advice in this chapter on when to abstract out a Single Source Of Truth is essentially the ideal intended outcome when the overly-simplistic advice "Don't Repeat Yourself" is issued.  In other words, a well-crafted Single Source Of Truth is 'DRY Done Right'.

To summarise:
1. Separate Concerns in the code base, so that the code now comprises of many individually coherent code modules.
2. If two (or more) code modules appear to have identical functionality, ask the question: "Could it ever be _correct_ for these two modules to diverge so they are no longer identical?"
3. If the answer is "Yes", then leave the two code modules alone.  Do not merge them.
4. If the answer is "No, for program correctness, these two code modules should always be identical", then Collate Concerns - merge the separate code modules into a Single Source Of Truth.
