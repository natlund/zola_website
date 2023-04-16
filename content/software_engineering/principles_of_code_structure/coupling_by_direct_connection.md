+++
title = "Coupling By Direct Connection"
date = 2023-04-16
weight = 132
+++

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
