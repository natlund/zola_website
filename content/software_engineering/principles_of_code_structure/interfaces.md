+++
title = "Interfaces - The Glue That Connects"
date = 2022-12-19
weight = 170
+++

# Interfaces: The Glue That Connects

An **interface** to a code module is the point of entry.  Examples include:
* A function call.  The interface is defined by the function name and signature (arguments passed in).
* Class instantiation, and the suite of public methods on the object.
* Internet requests via the `http` protocol.

An Application Programming Interface (API) is any interface that a programmer could use, by learning the protocol, and writing correct code for it.  In practice, the words 'API' and 'interface' are generally used interchangeably.

An interface may be private or public.  Somewhat different guidelines apply between private and public interfaces.

#### Private Interfaces

Private interfaces can be modified without external consequence.  Furthermore, private interfaces _should_ be modified as the program iterates towards a sound structure engineered for readability.  The _ideal_ interface should emerge organically as the program is developed.

#### Public Interfaces

Any interface that an external party uses is _public_.  Therefore, modifying the interface will affect the external party.  If the external party is just some engineers on the other side of the office, then this can be coordinated.  However, if the external party could be any random user on the internet, then more care is required.

In general, a public interface should be **versioned**, so that if it is changed, the change is explicitly advertised.

A public interface needs _much_ more care in its design than a private interface, because it is much harder to change.

### API Design

#### Multi-Granular

Especially for a non-trival public API, the interface should have **different levels of granularity**.  This means:

1. **Atomic operations** should be defined and exposed.  These are the lowest-level building blocks of API operations.  This is the lowest level of granularity.  The atomic operations should form a **complete set**, so that any possible action with the API can be achieved by a sequence of atomic operations.

2. **Routine operations** should be possible with a single simple call.  That is, the most common uses of the API should be _trivial_ to achieve.  Internally, each routine operation should use atomic operations, so that by definition, a routine operation call is equivalent to a sequence of atomic operation calls.

3. Further operations should be defined _very sparingly_.  Outside of the full set of atomic operations, and operations for the commonest use cases, it is wise to be very reluctant to add any more.  Further operations add confusing bloat to the API, and are a maintenance burden, both of which are costs that are probably greater than the value of adding an API call for some obscure operation.

#### Consider Using Specification Data Objects

Suppose you are developing a function that is turning out to have rather a lot of parameters.  The function call is becoming unwieldy.  Furthermore, many of those parameters must be further passed down into sub-functions, that are themselves suffering a bloated signature.

Now, this _may_ be a sign of a bad abstraction - is the function trying to do much?  Should it be broken into separate concerns?  However, let us assume that it is indeed a good abstraction, and the entry point really does require that many parameters, due to the nature of the domain problem.

One solution is to modify the function signature to accept a single rich data object, instead of a multitude of low-level parameters.  The 'parameter space' is thought of as a separate concern that can be abstracted out into a data object.  Generally, this abstraction will represent a _specification_ for the algorithm that the function carries out.  This spec object can be easily passed down into sub-functions, which tends to significantly tidy up code.

One possible benefit of this approach is that the _effective_ signature of the function can be changed _without_ actually changing the function signature, by simply modifying the structure of the specification data object.  Of course, changing the spec object may cause its own problems: strictly speaking, we are still changing the API.  But the hope is that this form of change will be easier than changing the function call itself.

This advice on API design is an example of the application of previous advice to separate state into its own object, since objects are perfectly suited for data-like code.
