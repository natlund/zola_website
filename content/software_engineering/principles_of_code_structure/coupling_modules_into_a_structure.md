+++
title = "Coupling Modules Into A Structure"
date = 2022-12-19
weight = 180
+++

# Coupling Modules Into A Structure

### A Couple Of Structures: Tree And Linear

Connecting modules together produces a structure that can be considered to be a network of nodes and links (or 'edges').  (The mathematical field of _graph theory_ is the study of these structures and their properties.)

While there are an infinite number of possible structures, a couple of foundational 'platonic forms' will be familiar: trees and chains.  They are intuitive enough that diagrams will be sufficient reminders of their definitions.

#### Chain (Linear structure)

<svg width="500" height="40">
    <line x1="25" y1="20" x2="475" y2="20" stroke="red" stroke-width="8"/>
    <circle cx="25" cy="20" r="20" fill="blue"/>
    <circle cx="175" cy="20" r="20" fill="blue"/>
    <circle cx="325" cy="20" r="20" fill="blue"/>
    <circle cx="475" cy="20" r="20" fill="blue"/>    
</svg>


#### Tree

<svg width="500" height="340">
    <line x1="250" y1="20" x2="100" y2="170" stroke="red" stroke-width="8"/>
    <line x1="250" y1="20" x2="400" y2="170" stroke="red" stroke-width="8"/>
    <line x1="100" y1="170" x2="25" y2="325" stroke="red" stroke-width="8"/>
    <line x1="100" y1="170" x2="175" y2="325" stroke="red" stroke-width="8"/>
    <line x1="400" y1="170" x2="325" y2="325" stroke="red" stroke-width="8"/>
    <line x1="400" y1="170" x2="475" y2="325" stroke="red" stroke-width="8"/>
    <circle cx="250" cy="20" r="20" fill="blue"/>
    <circle cx="100" cy="170" r="20" fill="blue"/>
    <circle cx="400" cy="170" r="20" fill="blue"/>
    <circle cx="25" cy="320" r="20" fill="blue"/>
    <circle cx="175" cy="320" r="20" fill="blue"/>
    <circle cx="325" cy="320" r="20" fill="blue"/>
    <circle cx="475" cy="320" r="20" fill="blue"/>    
</svg>
