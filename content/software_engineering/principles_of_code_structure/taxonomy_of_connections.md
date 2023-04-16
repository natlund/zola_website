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

Some specific forms of connection, in approximate order of simplicity.

1. Function call.
2. Method call on class.
3. Object instantiation, then method call on object.
4. Function call of injected function.
5. Method call on injected object.
6. Inheritance.  Method call on parent class.

These may be grouped into three different types:

- Coupling By Direct Connection
  - Function call
  - Method call on class
  - Object instantiation, then method call on object
- Coupling By Dependency Injection
  - Function call of injected function
  - Method call on injected object
- Inheritance
  - Method call on parent class

In the next three chapters, we'll look at these forms of connection.  We'll make some observations on the relative simplicity of each form.

As well as simplicity, we are also interested in how each connection type supports modularity.  The 'replacement' type of modification is arguably the simplest, and the syntax is essentially the same as for 'simple extension', so we shall analyse the 'replaceability' of each connection form.
