+++
title = "Collate The Concern Of Logical Branching"
date = 2022-12-19
weight = 110
+++

# Collate The Concern Of Logical Branching

If your code requires a logical branch, try to do it only once.  Your code will be much cleaner and easier to read.

Making the _same_ logical branch (i.e. exactly the same logical conditions) in _multiple_ places should be considered an anti-pattern, or at least a code smell.  The resulting code is always cluttered and messy.  Try to refactor it to have only one occurrence of the logical branch.

In graphical form, the left hand pattern is much easier to understand than the right hand pattern:

<div align="center">
<svg width="600" height="640">
    <line x1="100" y1="20" x2="100" y2="120" stroke="red" stroke-width="8"/>
    <line x1="100" y1="120" x2="20" y2="220" stroke="red" stroke-width="8"/>
    <line x1="100" y1="120" x2="180" y2="220" stroke="red" stroke-width="8"/>
    <line x1="20" y1="220" x2="20" y2="620" stroke="red" stroke-width="8"/>
    <line x1="180" y1="220" x2="180" y2="620" stroke="red" stroke-width="8"/>
    <circle cx="100" cy="20" r="20" fill="blue"/>
    <polygon points="100,90 70,120 100,150 130,120" fill="lime" stroke="black"/>
    <circle cx="20" cy="220" r="20" fill="blue"/>
    <circle cx="20" cy="320" r="20" fill="blue"/>
    <circle cx="20" cy="420" r="20" fill="blue"/>
    <circle cx="20" cy="520" r="20" fill="blue"/>    
    <circle cx="20" cy="620" r="20" fill="blue"/>    
    <circle cx="180" cy="220" r="20" fill="blue"/>
    <circle cx="180" cy="320" r="20" fill="blue"/>
    <circle cx="180" cy="420" r="20" fill="blue"/>
    <circle cx="180" cy="520" r="20" fill="blue"/>
    <circle cx="180" cy="620" r="20" fill="blue"/>
    <line x1="500" y1="20" x2="500" y2="120" stroke="red" stroke-width="8"/>
    <line x1="500" y1="120" x2="420" y2="220" stroke="red" stroke-width="8"/>
    <line x1="500" y1="120" x2="580" y2="220" stroke="red" stroke-width="8"/>
    <line x1="420" y1="220" x2="500" y2="320" stroke="red" stroke-width="8"/>
    <line x1="580" y1="220" x2="500" y2="320" stroke="red" stroke-width="8"/>
    <line x1="500" y1="320" x2="500" y2="420" stroke="red" stroke-width="8"/>
    <line x1="500" y1="420" x2="420" y2="520" stroke="red" stroke-width="8"/>
    <line x1="500" y1="420" x2="580" y2="520" stroke="red" stroke-width="8"/>
    <line x1="420" y1="520" x2="500" y2="620" stroke="red" stroke-width="8"/>
    <line x1="580" y1="520" x2="500" y2="620" stroke="red" stroke-width="8"/>
    <circle cx="500" cy="20" r="20" fill="blue"/>
    <polygon points="500,90 470,120 500,150 530,120" fill="lime" stroke="black"/>
    <circle cx="420" cy="220" r="20" fill="blue"/>
    <circle cx="500" cy="320" r="20" fill="blue"/>
    <polygon points="500,390 470,420 500,450 530,420" fill="lime" stroke="black"/>
    <circle cx="420" cy="520" r="20" fill="blue"/>    
    <circle cx="580" cy="220" r="20" fill="blue"/>
    <circle cx="580" cy="520" r="20" fill="blue"/>    
    <circle cx="500" cy="620" r="20" fill="blue"/>
</svg>
</div>

### Make Branching Explicit

One (misguided) way to save a line of code is to write a logical branch like this:
```py
x = 0  # Default value.
if some_condition is True:
    x = 1
```
Now, does this _look_ like a logical branch?  At first glance, the reader notices that a variable is set, then mutated _if_ a particular condition is true.  The pattern is: 1) Do some work. 2) If a condition is true, then _undo and redo_ the work.

What does mutating a variable have to do with logical branching?  The answer is: _nothing_.  This mutation is not necessary to achieve logical branching.  In fact, while all languages allow logical branching, there are modern languages with an emphasis on safety that strongly discourage mutation, or even forbid it.  (Eg. Rust, and functional languages.)  Mutation typically makes code harder to reason about, so should be kept to an absolute minimum.

The _meaning_ of the code is: make a binary logical choice.  Therefore, the code should reflect that meaning as directly as possible.  The traditional `if else` construction does this perfectly:
```py
if some_condition is True:
    x = 1
else:
    x = 0
```
The other benefit of the traditional `if else` is that the code at the same _logical level_ (down one branch or the other) is at the same _indentation level_.

In the diagrams below, the _meaning_ of the code is shown as the tree with red links, and the _execution flow_ of the code is shown as the black arrows.

<div align="center">
<svg width="600" height="260">
    <defs>
        <marker id="arrowhead" markerWidth="10" markerHeight="8" 
         refX="8" refY="4" orient="auto">
            <polygon points="2 4, 0 8, 10 4, 0 0"/>
    </defs>
    <-- Left hand tree -->
    <line x1="100" y1="20" x2="100" y2="120" stroke="red" stroke-width="8"/>
    <line x1="100" y1="120" x2="20" y2="220" stroke="red" stroke-width="8"/>
    <line x1="100" y1="120" x2="180" y2="220" stroke="red" stroke-width="8"/>
    <circle cx="100" cy="20" r="20" fill="blue"/>
    <polygon points="100,90 70,120 100,150 130,120" fill="lime" stroke="black"/>
    <circle cx="20" cy="220" r="20" fill="blue"/>
    <circle cx="180" cy="220" r="20" fill="blue"/>
    <text x="0" y="260">x = 0</text>
    <text x="160" y="260">x = 1</text>
    <--   Flow arrows -->
    <line x1="20" y1="0" x2="20" y2="195" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="43" y1="217" x2="95" y2="155" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="105" y1="155" x2="155" y2="215" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <-- Right hand tree -->
    <line x1="500" y1="20" x2="500" y2="120" stroke="red" stroke-width="8"/>
    <line x1="500" y1="120" x2="420" y2="220" stroke="red" stroke-width="8"/>
    <line x1="500" y1="120" x2="580" y2="220" stroke="red" stroke-width="8"/>
    <circle cx="500" cy="20" r="20" fill="blue"/>
    <polygon points="500,90 470,120 500,150 530,120" fill="lime" stroke="black"/>
    <circle cx="420" cy="220" r="20" fill="blue"/>
    <circle cx="580" cy="220" r="20" fill="blue"/>
    <text x="400" y="260">x = 0</text>
    <text x="560" y="260">x = 1</text>
    <-- Flow arrows -->
    <line x1="530" y1="0" x2="530" y2="115" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="527" y1="127" x2="580" y2="195" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
</svg>
</div>

The left-hand diagram of the code using mutation shows how the code actually traverses one branch of the tree _before_ encountering the conditional.  This disconnect from the semantics of the code has a cognitive cost.  So the 'shorter' method using variable mutation is actually harder to understand.  Don't try to save a single line of code at the expense of readability.  Just use the traditional `if else` construction.

### Use Polymorphism To Eliminate Logical Branching
Consider this code, a toy example of part of some kind of graphics program.  It may not be realistic, but it illustrates a point.
```py
class Square:
    def _init_(width):
        self.width = width


class Circle:
    def _init(radius):
        self.radius = radius


def calculate_total_area_of_shapes(shapes: list):
    total_area = 0

    for shape in shapes:
        if isinstance(shape, Square):
            total_area += area_of_square(shape)

        elif isinstance(shape, Circle):
            total_area += area_of_circle(shape)

        else:
            print("Shape not recognised.  Cannot calculate area.")

    return total_area


def area_of_square(square: Square):
    return square.width ** 2


def area_of_circle(circle: Circle):
    return 3.141592654 * circle.radius ** 2
```
The important point to note is the **logical branching** in the function `calculate_total_area_of_shapes()`.

This example code can also be considered a canonical example of the value of _method polymorphism_.  Let us rewrite the code to use method polymorphism.

```py
class Square:
    def _init_(width):
        self.width = width

    def area(self):
        return self.width ** 2


class Circle:
    def _init_(radius):
        self.radius = radius

    def area(self):
        return 3.141592654 * self.radius ** 2


def calculate_total_area_of_shapes(shapes: list):
    total_area = 0

    for shape in shapes:
        total_area += shape.area()

    return total_area
```
The code has been simplified considerably, and is easier to read.  This shows the value of method polymorphism.

But let's dig a little deeper.  Obviously, the two functions for calculating area have been _moved_ to be attached to the data structures they operate on. And the main function `calculate_total_area_of_shapes()` is drastically simpler because it no longer contains the logical branching.  Was it moved?  Upon inspection, the **logical branching** has apparently completely **disappeared** from our code!  Where did it go? In fact, the logical branching is still inside the compiled (byte) code in the form of look-up table or similar.  Method polymorphism has allowed us remove the logical branching from our source code, where it adds complexity for the human reader, and move it into the compiled code, where it is completely out of our sight, and now the responsibility of the computer.

Removing the complexity of logical branching from our source code is perhaps an under-appreciated aspect of object-oriented techniques such as this.
