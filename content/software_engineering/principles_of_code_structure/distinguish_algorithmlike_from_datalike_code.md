+++
title = "Distinguish Algorithm-like From Data-like Code"
date = 2022-12-19
weight = 80
+++

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
