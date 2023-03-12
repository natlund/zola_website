+++
title = "Separate Inherent And Collateral Complexity"
date = 2022-12-19
weight = 60
+++

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
