+++
title = "Make Execution Flow Obvious"
date = 2022-12-19
weight = 190
+++

# Make Execution Flow Obvious

Four paragraphs appearing at the beginning of the chapter [_Distinguish Algorithm-like From Data-like Code_](@/software_engineering/principles_of_code_structure/distinguish_algorithmlike_from_datalike_code.md) apply here.  For convenience, we repeat them verbatim here:

Time is linear.  Time is just one damn thing after another.

Important corollary: The execution of a computer program is a _sequence_ of operations, one after the other.  We can say that program flow is _linear_.

Even more important corollary:  Reading is a linear process.  We read one element at a time, _incrementally_ building an understanding of the whole piece.

Thus, to answer "what does this code do?" is to understand the sequence of operations during the execution of the code.  Furthermore, our understanding of that sequence of operations is built by reading parts of the code, one after the other.

Therefore, a key principle for structuring code for readability is: **make execution flow obvious**.

Before exploring how to apply this principle, we shall first deal with the _exception_ - code that _does not_ have a meaningful execution order, which we have defined as 'data-like code'.

## Data-like Code Favours A Tree Structure

Data can be thought of as just a bunch of static variables.  However, the variables may be grouped in various ways, and the groups themselves may be further grouped into higher-order sets, forming a **hierarchy**.  Thus, a **tree-like** structure can be imposed onto the bunch of variables.  If the data is correctly abstracted in this way, it will make more logical sense, and be easier to understand.

Obviously, code whose main purpose is to represent data should be structured so as represent the abstract tree of variable groupings.  Then, accessing the data in the rest of the program will be as intuitive and logical as possible.

Consider an example of some data in JSON format.  The first example shows data in 'flat' format.
```json
{
    "student_id": 12345678,
    "name": "Joe Aloysius Bloggs",
    "email": "j.bloggs@gmail.com",
    "phone": 07412345678,
    "street_address": "21 Jump Street",
    "town": "Crapstone",
    "county": "Devon",
    "postcode": "PL20 7PJ",
    "bank": "Barclays",
    "account_name": "J A Bloggs",
    "sort_code": "12-34-56",
    "account_number": "87654321",
}
```
The second example shows the same data grouped into a sensible tree structure.
```json
{
    "student_id": 12345678,
    "name": "Joe Aloysius Bloggs",
    "contact_details": {
        "email": "j.bloggs@gmail.com",
        "phone": 07412345678,
        "postal_address": {
            "street_address": "21 Jump Street",
            "town": "Crapstone",
            "county": "Devon",
            "postcode": "PL20 7PJ",
        }
    },
    "bank_details": {
        "bank": "Barclays",
        "account_name": "J A Bloggs",
        "sort_code": "12-34-56",
        "account_number": "87654321",
    }
}
```
The second example with the tree structure is obviously _much_ easier to parse.

Suppose the JSON example above needs to be represented as a data structure in a computer program.  There are various ways of converting JSON into, for example, a composition of objects.  The details of that conversion are not important here - what is important is that the organised tree structure is preserved.  Assuming that details of reading and converting the JSON are abstracted away, then (Python) code that uses the data structure could look like this:
```py
student_json = read_student_json()
student = convert_json_to_student_object(student_json)

...

email = student.contact_details.email

...

postcode = student.contact_details.postal_address.postcode

```
As we can see, the tree structure is accessed in an intuitive way using the nested 'dot' syntax of object attributes.

The logical grouping and sub-grouping of all the data elements makes the data structure easy to understand and work with.  So favour tree-like structures for data-like code.

## A Fundamental Cause Of Badly-Structured Code

Now that we have seen how tree-like code structures can be a great idea, let us indulge in a rant about how tree-like structures can be a _terrible_ idea. 

Why do intelligent people write such obfuscated, tangled code?  Here is one reason:

They are organising code as if it were nothing more than a static bunch of text statements.  Of course, it _is_ a static bunch text statements, but crucially, it may be _more_ than that: there is another dimension to consider.  We'll come back to this point.

The intelligent but unwise programmer looks at code as a bunch of static text statements, and proceeds to 'organise' it.  The programmer abstracts out an underlying logical structure, and breaks the code into separate parts.  He or she carries on, further breaking each newly-created part into separate logical chunks.  The final result is a large number of separate pieces, all connected together in a **tree** structure.  The intelligent but unwise programmer is probably proud of this achievement, believing that he or she has cleverly followed the Separation Of Concerns Principle to the letter.  The code is now so beautifully _organised_.

Now, as we have seen, this is eminently appropriate as long as the code is **data-like**.

But most code in an application is algorithm-like. For algorithm-like code, this approach is completely and utterly wrong.  As we noted above, there is another dimension: time.  More specifically: execution order.

Algorithm-like code consists of a series of actions performed in a sequence.  To understand the code, one must understand the exact sequence of actions.  A linear type of structure obviously perfectly captures the sequence of actions.  On the other hand, a tree structure _obfuscates_ the sequence of actions.


## Algorithm-like Code Suits Linear Structures


As the preceding sections have made clear, linear-type code structures maximise the readability of algorithm-like code.  Let us consider a plan of attack for achieving well-structured code, using our skills of software abstraction to separate concerns.

Practical Advice:
1)  Most code follows the pattern handed down from the ancients: Take some data, do things to the data, put the data somewhere.
2)  Assume we are considering a non-trivial algorithm of this type, that takes up more than one screen of code to implement.
3)  Take the entire algorithm, and decide what the different *logical* elements are.  A logical element does *one thing*, it is a logically distinct operation.  This breakdown has nothing to do with the number of lines of code: Some operations can be done in one line of code, others in one thousand.  In other words, _separate concerns._
4) Create a separate function to do each logical element.  Because of the clean logical separation, it should be easy to give the function an accurate and complete self-documenting name.
5) Now the entry point, the algorithm in question, can be written as a 'main' or 'orchestrator' function containing a linear sequence of sub-functions.

Now, code is fractal: each logical element described above may itself be composed of distinct logical sub-elements.  The same principle applies at any level: for each element, write code that clearly reveals the flow of execution order.

Because of the fractal nature, we end up with code that has a nested structure, and is therefore tree-like in some sense.  However, the structure is _not_ a 'pure' tree - there is a critical additional property: The _linearity_ of each element means that an explicit _execution flow_ can be traced through the structure.

The diagram below illustrates the 'nested chain' structure.  The black arrows show the execution flow.

<div align="center">
<svg width="400" height="640">
    <defs>
<!--         <marker id="arrowhead" markerWidth="10" markerHeight="8" 
         refX="8" refY="4" orient="auto">
            <polygon points="2 4, 0 8, 10 4, 0 0"/>
        </marker>  TO DO: Tweak placement of arrows now that smaller arrowhead is used.
 -->       
        <marker
            id="arrowhead"
            markerWidth="7" markerHeight="7" 
            refX="6" refY="3.5"
            orient="auto"
        >
            <polygon points="2.33 3.5, 0 7, 7 3.5, 0 0"/>
        </marker>
    </defs>
    <-- Main function -->
    <line x1="20" y1="20" x2="20" y2="620" stroke="red" stroke-width="8"/>
    <line x1="20" y1="220" x2="200" y2="120" stroke="red" stroke-width="8"/>
    <line x1="20" y1="220" x2="200" y2="320" stroke="red" stroke-width="8"/>
    <line x1="200" y1="120" x2="200" y2="320" stroke="red" stroke-width="8"/>
    <line x1="200" y1="253" x2="350" y2="187" stroke="red" stroke-width="8"/>
    <line x1="200" y1="253" x2="350" y2="320" stroke="red" stroke-width="8"/>
    <line x1="350" y1="187" x2="350" y2="320" stroke="red" stroke-width="8"/>
    <line x1="20" y1="520" x2="170" y2="453" stroke="red" stroke-width="8"/>
    <line x1="20" y1="520" x2="170" y2="587" stroke="red" stroke-width="8"/>
    <line x1="170" y1="453" x2="170" y2="587" stroke="red" stroke-width="8"/>
    <circle cx="20" cy="20" r="20" fill="blue"/>
    <circle cx="20" cy="120" r="20" fill="blue"/>
    <circle cx="20" cy="220" r="20" fill="blue"/>
    <circle cx="20" cy="320" r="20" fill="blue"/>
    <circle cx="20" cy="420" r="20" fill="blue"/>
    <circle cx="20" cy="520" r="20" fill="blue"/>
    <circle cx="20" cy="620" r="20" fill="blue"/>
    <-- Sub-function 1 -->
    <circle cx="200" cy="120" r="15" fill="blue"/>
    <circle cx="200" cy="187" r="15" fill="blue"/>
    <circle cx="200" cy="253" r="15" fill="blue"/>
    <circle cx="200" cy="320" r="15" fill="blue"/>
    <-- Sub-sub-function -->
    <circle cx="350" cy="187" r="15" fill="blue"/>
    <circle cx="350" cy="253" r="15" fill="blue"/>
    <circle cx="350" cy="320" r="15" fill="blue"/>
    <-- Sub-function 2 -->
    <circle cx="170" cy="453" r="15" fill="blue"/>
    <circle cx="170" cy="520" r="15" fill="blue"/>
    <circle cx="170" cy="587" r="15" fill="blue"/>
    <--   Flow arrows -->
    <line x1="50" y1="0" x2="50" y2="185" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="60" y1="182" x2="180" y2="115" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="225" y1="120" x2="225" y2="220" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="235" y1="212" x2="330" y2="172" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="375" y1="187" x2="375" y2="320" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="350" y1="345" x2="220" y2="280" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="220" y1="290" x2="220" y2="320" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="200" y1="345" x2="40" y2="250" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="50" y1="270" x2="50" y2="450" stroke="black" stroke-width="2" marker-end="url(#arrowhead)"/>
    <text x="37" y="475">Etc</text>
</svg>
</div>

An example sketch in Python would look something like:
```py
def main():
    config = read_config()
    data = load_data_from_file(config)
    transformed_data = operation_1(data)
    ...
    ...
    discombobulated_data = operation_4(transmogrified_data)
    ...


def operation_1(data):
    modified_data = sub_operation_1(data)
    ...
    mangled_data = sub_operation_3(altered_data)
    ...


def sub_operation_3(data):
    mutated_data = sub_sub_operation_1()
    ...


# Et cetera.
```

As noted in the section above [_A Fundamental Cause Of Badly-Structured Code_](@/software_engineering/principles_of_code_structure/make_execution_flow_obvious.md#a-fundamental-cause-of-badly-structured-code), the point is _not_ to create a neatly-structured tree of nodes, with each node having minimal content, resulting in a very deep tree.  Therefore, resist the temptation to group the functions into higher-level functions with vague names like `transform()`.  This incredibly widespread plague of abstraction addiction is the *opposite* of writing readable code.

Furthermore, as noted in the chapter [_Separate Input/Output From Computation_](@/software_engineering/principles_of_code_structure/separate_input_output_from_computation.md), Input dependencies such as reading a configuration file, reading environment variables from the operating system, loading a data file, _etc_, should happen at the **start** of the algorithm.  Making dependencies obvious is an important part of making code easy to understand quickly, so declare them up front. 


### The Daisy-Chain Anti-Pattern

Code with a 'daisy-chain' structure has a _linear_ structure, but lacks a proper 'main' or 'orchestrator' function.  Code consists of a chain of function calls, where each function calls the next function in the sequence, instead of returning back up to an orchestrator.  There are two main flaws of this structure:

1. With no 'main' or orchestrator function, the overall structure of the algorithm cannot be seen anywhere.  One must read all the functions in turn to build a mental picture of the key steps in the algorithm.
2. The entry point will be the first function in the sequence.  Since it will have a single clear concern, it should have a simple descriptive name such as `read_data_file()`.  However, its final act is to call the next function in the sequence, thus ultimately executing the entire program.  Executing the entire program is the _mother_ of all side-effects for a simple function!

So don't do this.  Instead, use the (nested) linear structures with orchestrators described in the previous section.

The example sketch above structured in this anti-pattern would look something like this:
```py
def read_config():
    ...
    load_data_from_file(config)


def load_data_from_file(config):
    ...
    operation_1(data)


def operation_1(data):
    ...
    operation_2(data):


def operation_2(data):
    ...
    operation_3(data)
```

## Summary

The structure of code should reflect its purpose.  Is the purpose of a module of code to store data or is it to do some computation?

Note that a data-like code component may still have algorithm-like code within it, for example, non-trivial accessor methods on a complex data structure.  Within those accessor methods, the advice for algorithm-like code applies (favour linear 'nested chain' structures).

> **Code should look like what it is.  Code should look like what it does.**
