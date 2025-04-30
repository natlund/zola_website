+++
title = "Miscellaneous Advice"
date = 2022-12-19
weight = 220
+++

# Miscellaneous Advice

Some advice on low-level code constructions that nevertheless have a big impact on code readability.

##  Name Things Clearly

Everything in your code should have a name that is precise, descriptive, and at the appropriate level of abstraction.  Then your code can be said to be _self-documenting_.  If the reader trusts that all names have been chosen with care, then the reader can understand the code much more quickly because the names describe what each piece is and does.  Self-documenting code also needs fewer comments to explain the code.

However, naming things is _hard_.  The skill of naming things well takes a long time to develop.  Perhaps this skill is one signifier of a 'senior engineer'.  Here are some guidelines to consider when trying to find a suitable name.

For clarity, consider a simple floating-point number variable that needs a self-documenting name.  The variable name could:
1. Describe **where it comes from**, or how it was constructed.  For example, a variable computed from the sum some financial transactions could be called `sum_of_transactions`.
2. Describe **where it's going** - what it will be **used for**.  For example, if the variable is fed into a function that ultimately generates a financial statement, then an appropriate name could be `sum_for_statement_generator`.
3. Describe what is **is**, in the sense of 'what it means, in the context of the problem domain'.  For example, if the variable _actually_ represents net profit, then an obvious candidate name would be `net_profit`.

Options 1 and 2 (**where it comes from** or **where it's going**) are the easiest to work with.  Either one would likely add _considerably_ more value than a vague variable name such as `val`.

However, Option 3 - what it **is** - is likely to be the most valuable.  Describing the _meaning_ of a variable, _why it matters_, will generally give the most insight into what the code as a whole is supposed to achieve.  But this is also generally the most difficult option to implement: It requires a proper understanding of the problem domain, and the skill at seeing the correct level of abstraction to describe this small part of the domain.

Naming things is _hard_.  But the payoff of good, self-documenting variable names is huge, so persevere in finding them.


## Code Hygiene

The phrase 'code hygiene' is sometimes used to refer to the practice of cleaning up temporary files and other sundry mess resulting from software development, and keeping necessary configuration files _etc_ in a tidy state.  The idea is to keep your engineering workspace in a state that minimises confusion.  A few hints follow.

Don't call a file `data.txt`.  Call it what it is.  Spend 60 seconds thinking of a great name.  This will save _many minutes_ in the future.  So call it something like `user_accounts_2023-01-21.txt`

Delete temporary files as soon as you can.  They are supposed to be _temporary_.

A common problem is that you can't delete a temporary file immediately, because you may need it again in a few hours or days.  So try this trick:  Put a deletion date in the file name. Eg.

`user_accounts_2023-01-21_DELETE_AFTER_2023-02-01.txt`

Then, in six months time, when you stumble across this long-dead file again, you won't have to spend time investigating whether or not it is safe to delete.


## Mistake Proof With Types

Consider a couple of variables that are **integers**, and encode something like Customer IDs or Product IDs.  Now consider some function that takes _both_ variables.  Something like this in Python:
```py
def some_function(product_id: int, customer_id: int):
	...


product_id = 1234
customer_id = 5678

result = some_function(product_id, customer_id)
```

Now suppose that the two variables were accidentally interchanged in the function invocation.  If the Customer ID number happened to be a legitimate Product ID, and vice versa, then the function call would succeed.  But obviously the result returned would _not_ be the intended one.  Because nothing has 'failed', this logic bug could go unnoticed, causing weird problems for a long time.
```py
wrong_result = some_function(customer_id, product_id)  # Bug! Arguments swapped.
```

Here's a tactic to reduce these subtle logic bugs by 'mistake-proofing' the function call:  Create _explicit_ data types for Product ID _etc_, that inherit from the simple integer type.  Then specify the new types as the types of the arguments of the function.  Finally, use the appropriate data type at the point the variables are created.  That way, the language's type system (or type hinting) can prevent (or warn against) the use of the wrong arguments in the function call.  In Python, something like this would suffice:
```py
class ProductID(int):  # Inherits from integer.
	def __init__(self, value):
		pass


class CustomerID(int):  # Inherits from integer.
	def __init__(self, value):
		pass


def some_function(product_id: ProductID, customer_id: CustomerID):
	...


product_id = ProductID(1234)
customer_id = CustomerID(5678)

result = some_function(product_id, customer_id)
``` 

In a statically-typed language, the compiler would prevent the accidental use of say, a CustomerID in place of a ProductID.  Some dynamically-typed languages, such as Python, now have type _hinting_.  Modern IDEs use type hints to loudly warn against the use of the wrong types, so the programmer can immediately see the bug while writing the code.

There is a little extra overhead from defining the new types.  But in large systems, where the variables are passed a long way around, mistake proofing with types is likely to be a net benefit.


## Use Inclusive-Exclusive Ranges

Famed computer scientist Edsger Dijkstra wrote an essay in 1982 explaining why the best convention to describe a range of numbers is to have an **inclusive** lower bound and an **exclusive** upper bound.  In mathematics, this corresponds to the _half-open interval_ with a _closed_ lower bound and an _open_ upper bound, denoted `[a, b)`, where `a` is contained in the interval, but `b` is not.

To illustrate by example, a range of natural numbers defined by the pair `[3, 6)` denotes the numbers `[3, 4, 5]`.  In other words, the the lower bound (`3`) is **included** in the range, and the upper bound (`6`) is **excluded** from the range.


To summarise Dijkstra's reasoning:

1. The number of elements in the range is simply upper bound minus lower bound.  (This convenient arithmetic is not true for the inclusive/inclusive or exclusive/exclusive conventions.)

2. The lowest natural number, zero, can be included in a range, without having the lower bound go outside of the set of natural numbers.  (The lower bound is zero; it doesn't have to be eg. -1, as it might for the convention of an _exclusive_ lower bound.)

3. For two _adjacent_ ranges, the upper bound of one is the lower bound of the other.  So if one wants to define a new range 'starting from' an existing range, the lower bound is already known; no calculation is required.  (Without this convention, calculating the lower bound of the new adjacent range can be surprisingly non-trivial, especially for time ranges.)

Doctor Dijkstra goes on to say that all four conventions were tried in the Mesa programming language, and the empirical evidence showed that the other three conventions were "a constant source of clumsiness and mistakes".  The essay is well worth a read.

The value of Dijkstra's inclusive/exclusive convention is particularly clear when dealing with time spans.  Consider two adjacent time ranges in Dijkstra's convention: 1:00 - 2:00, 2:00 - 3:00.  Now try to express these ranges with the inclusive/inclusive convention.  What is the upper bound on the lower range? 1:59?  1:59:59?  What about milliseconds?  _Et cetera_.  The upper bound would depend on the resolution to which we measure time.  The same problem applies to the exclusive/exclusive convention.

So prefer Dijkstra's inclusive/exclusive convention for any ranges.
