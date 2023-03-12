+++
title = "Taxonomy Of Connections"
date = 2022-12-19
weight = 130
+++

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
