+++
title = "Coupling By Dependency Injection"
date = 2023-04-16
weight = 134
+++

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
