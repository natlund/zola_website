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

There are a few reasons why we should assess ease of modification:

Firstly, suppose we **know** that the code will need to be modified in the future.  Then the specification for the code will include the criterion "Needs to be easily modified".  So we choose the _most readable_ solution that provides the extensibility that we need.

Secondly, the label 'extensible' is often applied very vaguely.  Object-Oriented methods, in particular, are often claimed to be 'extensible', without much deep analysis as to how easy they actually are to extend, and whether they truly are easier to extend than simpler competing methods.  It is worth doing a little critical examination of this here.

Thirdly, 'swappable' modules must be loosely coupled, which tends to correlate with cleanly separated concerns.

Before continuing, let us explore some concrete meanings of 'extensible' and 'swappable'.

## Modifications: Replacements and Extensions

Suppose we have a piece of code, Module A, that calls another separate piece of code, Module B.  (Put another way, execution moves from Module A to Module B.)

<div align="center">
<svg width="500" height="70">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0"/>
        </marker>
    </defs>
    <rect x="5"   y="5" width="160" height="60" rx="15" stroke="black" fill="lime" />
    <text x="85" y="35" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="255" y="5" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="35" text-anchor="middle" alignment-baseline="central">Module B</text>
    <line x1="165" y1="35" x2="252" y2="35" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
</svg>
</div>

### Replacement

Now suppose we need to modify the code by replacing the functionality of Module B with new functionality.  The replacement functionality will be inside a new module Module C, and Module A will be modified to call Module C instead of Module B.

<div align="center">
<svg width="500" height="190">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0"/>
        </marker>
    </defs>
    <rect x="5"   y="125" width="160" height="60" rx="15" stroke="black" fill="lime" />
    <text x="85" y="155" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="255" y="5" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="35" text-anchor="middle" alignment-baseline="central">Module B</text>
    <rect x="255" y="125" width="160" height="60" rx="15" stroke="black" fill="violet" />
    <text x="335" y="155" text-anchor="middle" alignment-baseline="central">Module C</text>
    <line x1="165" y1="155" x2="252" y2="155" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
</svg>
</div>

Thus, Module B has been swapped for Module C.

### Simple Extension

Now, instead suppose we need to modify the code by adding extra functionality.  The extra functionality will be inside a new module Module C, and Module A will call Module C.

If the call to Module C is completely independent of the call the to Module B, then we can call this **simple extension**.

<div align="center">
<svg width="500" height="190">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0"/>
        </marker>
    </defs>
    <rect x="5"   y="5" width="160" height="180" rx="15" stroke="black" fill="lime" />
    <text x="85" y="95" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="255" y="5" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="35" text-anchor="middle" alignment-baseline="central">Module B</text>
    <line x1="165" y1="35" x2="252" y2="35" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
    <rect x="255" y="125" width="160" height="60" rx="15" stroke="black" fill="violet" />
    <text x="335" y="155" text-anchor="middle" alignment-baseline="central">Module C</text>
    <line x1="165" y1="155" x2="252" y2="155" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
</svg>
</div>

### Extension By Case

Finally, suppose that the code needs to be modified to add extra functionality, but the extra functionality is _not_ exactly independent of the existing functionality.  Assume the new functionality is in some sense _parallel_ to existing functionality, for example, the new functionality has been added to handle an extra _case_.

The new functionality will be in a new module Module C.  Then, Module A will call _either_ Module B _or_ Module C, depending on the case.

<div align="center">
<svg width="500" height="190">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0"/>
        </marker>
    </defs>
    <rect x="5"   y="5" width="160" height="180" rx="15" stroke="black" fill="lime" />
    <text x="85" y="95" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="255" y="5" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="35" text-anchor="middle" alignment-baseline="central">Module B</text>
    <line x1="165" y1="95" x2="252" y2="35" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
    <rect x="255" y="125" width="160" height="60" rx="15" stroke="black" fill="violet" />
    <text x="335" y="155" text-anchor="middle" alignment-baseline="central">Module C</text>
    <line x1="165" y1="95" x2="252" y2="155" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
</svg>
</div>

Thus, the code has been extended with Module C.

### Modularity

Code that is very easy to extend by connecting a new module, or can easily have existing modules replaced by new modules, is often described as **modular**.  Phrases like 'pluggable architecture' are also heard.

Modular code is very desirable from the standpoint of the maintenance and evolution of the code base.  But is it also readable?  Luckily, yes: modular code tends to have clean separation of concerns, and obviously has clean connections between components.  Such code has a strong chance of 'just making sense'. 

## Types Of Connections

Some types of connection, in approximate order of simplicity.

1. Function call.
2. Method call on class.
3. Object instantiation, then method call on object.
4. Function call of injected function.
5. Method call on injected object.
6. Inheritance.  Method call on parent class.

As well as simplicity, we are also interested in how each connection type supports modularity.  The 'replacement' type of modification is arguably the simplest, and the syntax is essentially the same as for 'simple extension', so we shall analyse 'replaceability' here.

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
As simple as possible.  The function call _is_ the connection.  The only coupling is a direct connection to an explicit module.

<div align="center">
<svg width="500" height="70">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0"/>
        </marker>
    </defs>
    <rect x="5"   y="5" width="160" height="60" rx="15" stroke="black" fill="lime" />
    <text x="85" y="35" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="255" y="5" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="35" text-anchor="middle" alignment-baseline="central">Function B</text>
    <line x1="165" y1="35" x2="252" y2="35" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
</svg>
</div>


#### Replaceability:
A new function `alternative()` must be written.  Then changing the coupling simply requires changing the function call in `main()`:
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
* Write new replacement function.
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

The method call _is_ the connection.  The only coupling is a direct connection to the explicit method of a class.

<div align="center">
<svg width="500" height=120">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0"/>
        </marker>
    </defs>
    <rect x="5"  y="45" width="160" height="60" rx="15" stroke="black" fill="lime" />
    <text x="85" y="75" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="250" y="5" width="170" height="105" rx="5" stroke="black" fill="gainsboro" />
    <text x="335" y="25" text-anchor="middle" alignment-baseline="central">Class B</text>
    <rect x="255" y="45" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="75" text-anchor="middle" alignment-baseline="central">Method C</text>
    <line x1="165" y1="75" x2="252" y2="75" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
</svg>
</div>

#### Replaceability:
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
* Write new replacement method or class.
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
No longer as simple as possible, but still straightforward.  There is the extra overhead of having to instantiate the container class.

The coupling now has two elements: instantiating the object, and calling the method on the object.  If both are done in the same place, then the coupling is trivial to understand.  However, if instantiation is done in a very different place to the method call, then the reader has to mentally keep track of both parts of the coupling to properly understand how Module A depends on Module B.

<div align="center">
<svg width="500" height=130">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0"/>
        </marker>
    </defs>
    <rect x="5"  y="10" width="160" height="120" rx="15" stroke="black" fill="lime" />
    <text x="85" y="70" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="250" y="5" width="170" height="125" rx="5" stroke="black" fill="thistle" />
    <text x="335" y="35" text-anchor="middle" alignment-baseline="central">Object B</text>
    <rect x="255" y="65" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="95" text-anchor="middle" alignment-baseline="central">Method C</text>
    <line x1="165" y1="35" x2="250" y2="35" stroke="black" stroke-width="6" />
    <line x1="165" y1="95" x2="252" y2="95" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
</svg>
</div>


#### Replaceability:
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

* Write new replacement method or class.
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
No longer simple.  There are now _three_ modules required.  However, each module is itself very simple.

The coupling consists of two elements: the Orchestrator passing Function B into Module A, and the call on Function B.  Worryingly, the two elements of coupling are _necessarily_ in different parts of the code.

The function call has been **anonymised**:  When reading the `main()` function alone, it is impossible to know what _real_ function the injected function actually is.  (In fact, An IDE would probably be unable to 'jump to source' of `injected_func`.)  We may say that the connection is **indirect** or abstract.

In order to fully understand the coupling, the reader needs to follow a function as it is passed around the code.  The complexity of indirect connection is a mental load on the reader.


<div align="center">
<svg width="500" height="190">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0" />
        </marker>
    </defs>
    <rect x="5"   y="5" width="410" height="60" rx="15" stroke="black" fill="gainsboro" />
    <text x="210" y="35" text-anchor="middle" alignment-baseline="central">Orchestrator</text>
    <rect x="5"   y="125" width="160" height="60" rx="15" stroke="black" fill="lime" />
    <text x="85" y="155" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="255" y="125" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="155" text-anchor="middle" alignment-baseline="central">Function B</text>
    <line x1="335" y1="125" x2="335" y2="65" stroke="gray" stroke-width="6" />
    <line x1="338" y1="65" x2="82" y2="65" stroke="gray" stroke-width="6" />
    <line x1="85" y1="65" x2="85" y2="125" stroke="gray" stroke-width="6" marker-end="url(#arrowhead)"/>
    <line x1="165" y1="155" x2="252" y2="155" stroke="black" stroke-width="6" stroke-dasharray="15 5" marker-end="url(#arrowhead)"/>
</svg>
</div>

#### Replaceability:
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
* Write new replacement function.
* One-line change in orchestrator function, to pass in alternative function.
* `main()` function is **not** changed.


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

Relatively complex.  There are now _three_ modules required.

The coupling consists of three elements:  the Orchestrator instantiating Object B, the Orchestrator passing Object B into Module A, and the call on Method C of Object B.  
Disturbingly, the method call is _necessarily_ in a different part of the code from the other elements of the coupling.

Note that while the object is anonymous, the method call is on the actual named method on the class.

This coupling pattern can manifest in a range of different ways, from perfectly readable to horrendously obfuscated, depending on how the _type_ (class) of the injected object is controlled.  Let's explore three of those ways.

##### Injected Object Has Single Fixed Class

First, consider the case where the injected object is _always_ an instance of a _single_ class.  The object may vary in its particulars, but there is only one bit of code to look at.  This should not pose any great problems for readability.

##### Injected Object Of Unknown Class But With Well-Defined Interface

Next, consider the case where the class of the injected object is unknown, but the method constitutes a _well-defined interface_, in the following sense: While the behaviour of the method necessarily changes depending on the class, the behaviour is always sufficiently well-constrained that the reader _does not_ really need to know about the detailed differences between the methods of the different classes.  In other words, the method call can always be treated as a call to a 'black box', whose inner workings do not matter to the reader trying to understand the code of Module A.

The method polymorphism used in this case should not pose a great problem for readability, _as long as_ the software design guarantees that the reader can always treat the method call as a call to a closed 'black box'.  In practice, it may be difficult to always achieve this.  If the reader _does_ end up needing to know the details inside a method, then this interface could be considered a 'leaky abstraction', at least from the reader's point of view, because the information hidden inside the abstraction 'leaks out'.

##### Injected Object Of Unknown Class

Finally, consider the case where the class of the injected object is unknown, and the reader simply _must_ read the details inside the method in order comprehend the code.

The method call on the object is an indirect connection:  When reading the `main()` function alone, it is impossible to know the real class of the injected object.  (In fact, An IDE will probably not be able to 'go to source' of `injected_object`.)

In order to fully understand the coupling, the reader needs to follow an object as it is passed around the code.  The complexity of indirect connection is a mental load on the reader.


<div align="center">
<svg width="500" height="255">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0" />
        </marker>
    </defs>
    <rect x="5"   y="5" width="415" height="60" rx="15" stroke="black" fill="gainsboro" />
    <text x="210" y="35" text-anchor="middle" alignment-baseline="central">Orchestrator</text>
    <rect x="5"   y="185" width="160" height="60" rx="15" stroke="black" fill="lime" />
    <text x="85" y="215" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="250" y="125" width="170" height="125" rx="5" stroke="black" fill="thistle" />
    <text x="335" y="155" text-anchor="middle" alignment-baseline="central">Object B</text>
    <rect x="255" y="185" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="335" y="215" text-anchor="middle" alignment-baseline="central">Method C</text>
    <line x1="364" y1="125" x2="364" y2="65" stroke="black" stroke-width="6" />
    <line x1="307" y1="125" x2="307" y2="65" stroke="gray" stroke-width="6" />
    <line x1="310" y1="65" x2="82" y2="65" stroke="gray" stroke-width="6" />
    <line x1="85" y1="65" x2="85" y2="185" stroke="gray" stroke-width="6" marker-end="url(#arrowhead)"/>
    <line x1="165" y1="215" x2="252" y2="215" stroke="black" stroke-width="6" stroke-dasharray="15 5" marker-end="url(#arrowhead)"/>
</svg>
</div>

#### Replaceability:
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
* Write new replacement class with different method _of same name_.
* One-line change in orchestrator function, to instantiate new class.
* `main()` function is **not** changed.

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

Relatively complex.  There are three modules, and the overhead of instantiating the container class.

The coupling consists of two elements: The direct connection of Method A calling Method B, and the potentially heavyweight connection of `MainClass` inheriting from `ParentClass`.

On the one hand, the connection via inheritance between the two modules is simpler than, say, 'Method Call On Injected Object', because the connection is explicitly hard-wired, rather than being dynamic.

On the other hand, the inheritance connection between `MainClass` and `ParentClass` couples _everything_ in `ParentClass` to `MainClass`.  If the class hierarchy has not been extremely well-designed, then `MainClass` will have access to lots of methods which have _nothing_ to do with the concern of `MainClass`.  The problem is that any coupling (even indirect) could be construed as indicating a dependency: the reader may reason that a module has access to methods because it _needs_ them.  The reader may waste time sorting out which base class methods are actually relevant to `MainClass`, and which simply get dragged along as a consequence of inheritance.

<div align="center">
<svg width="500" height=130">
    <defs>
        <marker
            id="arrowhead"
            markerWidth="3" markerHeight="3" 
            refX="2" refY="1.5"
            orient="auto"
        >
            <polygon points="1 1.5, 0 3, 3 1.5, 0 0"/>
        </marker>
    </defs>
    <rect x="5" y="5" width="170" height="125" rx="5" stroke="black" fill="gainsboro" />
    <text x="90" y="35" text-anchor="middle" alignment-baseline="central">Main Class</text>
    <rect x="10"  y="65" width="160" height="60" rx="15" stroke="black" fill="lime" />
    <text x="90" y="95" text-anchor="middle" alignment-baseline="central">Module A</text>
    <rect x="255" y="5" width="170" height="125" rx="5" stroke="black" fill="thistle" />
    <text x="340" y="35" text-anchor="middle" alignment-baseline="central">Parent Class</text>
    <rect x="260" y="65" width="160" height="60" rx="15" stroke="black" fill="cyan" />
    <text x="340" y="95" text-anchor="middle" alignment-baseline="central">Method B</text>
    <rect x="175" y="15" width="80" height="40" stroke="black" fill="thistle" />
    <line x1="170" y1="95" x2="257" y2="95" stroke="black" stroke-width="6" marker-end="url(#arrowhead)"/>
</svg>
</div>

#### Replaceability:
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
* Write new replacement method on parent class (base class).
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


## Summary

<table class="dense-table">
   <caption>Some Connections Between Software Modules</caption>
   <thead>
      <tr> <th><!--Blank--></th> <th>Simplicity</th>          <th>Replaceability</th> </tr>
   </thead>
   <tbody>
      <tr>
        <th>Function Call</th>
        <td>Simple as possible</td>
        <td><ul><li>New function</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Class Method Call</th>
        <td>Simple.<br>Class is namespace</td>
        <td><ul><li>New class or method</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Object Method Call</th>
        <td>Medium.<br>Overhead of instantiation</td>
        <td><ul><li>New class or method</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Injected Function Call</th>
        <td>Somewhat Complex.<br>Three modules, but each<br>module is simple</td>
        <td><ul><li>New function</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Injected Object<br>Method Call</th>
        <td>Complex.<br>Three modules.<br>Overhead of instantiation</td>
        <td><ul><li>New class</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Inheritance</th>
        <td>Complex.<br>Three modules.<br>Possible irrelevant<br>inherited connections</td>
        <td>Worst case:<ul><li>New parent class</li><li>Refactor class hierarchy</li><li>One-line change</li></ul></td>
     </tr>
   </tbody>
</table>


## Conclusions

Don't use inheritance.  Be _very_ careful with dependency injection.  Favour simple direct connections.
