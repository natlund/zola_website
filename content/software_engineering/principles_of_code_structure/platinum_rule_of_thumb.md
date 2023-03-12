+++
title = "The Platinum Rule Of Thumb"
date = 2022-12-19
weight = 40
+++


# The Twin Pillars: Separation Of Concerns and Clarity Of Coupling

The central skill of software engineering is to analyse the problem to figure out what the different aspects are, and how those aspects relate to each other.

More precisely, an 'aspect' of a programming problem is an _area of concern, or responsibility_ that can be abstracted from from it.

The first pillar of software engineering is to _separate the concerns_ into separate software modules (generally, functions or objects).

The second pillar of software engineering is to decide how the separate concerns will be connected.

The separated concerns and the coupling between them are two sides of the same coin.  They define the totality of your software architecture.  Deciding on what the concerns are and how they connect is what software architecture _is_.

## Platinum Rule Of Thumb

Break computer code into separate modules such that:
1. Each module deals with a single concern or responsibility.
2. The coupling between the modules is minimised.

To add more nuance: The coupling between modules should be made as clear and obvious as possible.  This is _often_ achieved by minimising the amount of coupling.
