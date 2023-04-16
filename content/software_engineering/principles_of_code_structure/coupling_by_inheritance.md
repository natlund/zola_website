+++
title = "Coupling By Inheritance"
date = 2023-04-16
weight = 136
+++

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
