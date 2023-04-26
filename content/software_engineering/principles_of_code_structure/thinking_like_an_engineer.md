+++
title = "Thinking Like An Engineer"
date = 2023-04-27
weight = 230
+++

# Thinking Like An Engineer

## Format Code Perfectly At All Times

Keep code formatting perfect at all times.  _Don't_ say to yourself "I'll come back and fix the formatting later."  Write your code in the same way that a professional chef would practise 'clean as you go' in a busy commercial kitchen.  This discipline helps instil both the attention to detail and sensitivity to structure that characterise a good engineering mind.

## Single Source Of Truth

At the beginning of this book, we observed that the advice "Don't Repeat Yourself" is too simplistic: abstracting out everything possible is usually not a good idea.  Following that, approximately the first half of this book was devoted to exploring a bunch of concerns that _should_ be abstracted out.  With all that now under our belt, let us look at a high-level principle of abstraction.

Consider a piece of code that is important to the correctness to the program as a whole.  It may not be very big - for example, it could be a single configuration variable, perhaps just a boolean flag.  Another example could be a function that does some mathematical calculation.

Now consider the situation where the code is _duplicated_ - there are (at least two) functionally identical pieces of code.  Now let's imagine that at some point in time, the two copies _diverge_ so that they are no longer identical - perhaps one copy was updated, but the other was forgotten.  Finally, let's assume that the divergence is a _bug_, the program as a whole is no longer correct.

So we have identified a class of vulnerabilities in software design.  The obvious solution is to _not have_ duplicates, but rather just have a **single** instance of the critical piece of code.  The single instance of critical code is known as the "Single Source Of Truth".

Note that the motivation behind having a Single Source Of Truth is robustness (bug prevention) rather than readability.  But having a Single Source Of Truth will often improve readability: code needs to be read only _once_ to be understood.  The reader will not find themselves wondering "Wait, is this code essentially the same as that other code I read earlier?"  Generally, readability only suffers when the advice is applied obsessively at every possible opportunity, manifesting as DRY Abstraction Addiction.

The philosophy of having a Single Source Of Truth applies far beyond just computer software.  Documentation, in particular, should be written with the philosophy in mind: things should be defined in one place.  More generally, all written materials should have a single source of truth.  Management and organisation structure benefit from having clear roles and responsibilities, with explicit boundaries on authority.  An engineer cannot serve two masters...  (Your author once served _five_ masters at the same time.)

## Be Explicit

When reviewing computer code or working with another engineer, the phrase I find myself using the most often is "Be Explicit", and variations thereof.  Let me as the reader know _exactly_ what I need to know to understand what is going on.  Don't make me guess - crush ambiguity.  Express Intent: tell the reader what the code is trying to achieve.

The corollary to this is to hide away stuff that isn't important - don't distract me with irrelevance.  Take great care in deciding what is _really_ important to understanding the algorithm, and bring it to the surface where the reader can see it.  So this principle circles back to the Art Of Abstraction first encountered at the beginning of this book.  The right abstractions (at the right level of abstraction) make your code _make sense_.  Therefore, carefully cultivate the skills of abstraction.
