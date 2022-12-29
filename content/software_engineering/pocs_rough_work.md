+++
title = "POCS Rough Work"
date = 2022-12-18
weight = 1
draft = true
+++

------------------------------
Rough Notes.  Some good ideas, but not properly formed.

# Anti-Patterns

### Peasant Abstraction Anti-Pattern
Implicitly defining a set as "the set of all things I need to do a particular thing".  This can lead to what I call the Workshop anti-pattern, which, if abused even further, becomes the Kitchen Sink anti-pattern.

For example:  You need a sandwich.

  * Good engineering:  Make the sandwich in one place, once, wrap it safely in a paper bag, and take it with you as you go about your day.
  * Workshop anti-pattern: Assemble a giant hamper containing: a loaf of bread, a bread-knife, butter, salami, a sharp knife to slice the salami, a jar of gherkins, a jar of mustard, a jar of Branston pickle, a whole lettuce, a kitchen sink with running water to wash the lettuce in, and a paper bag to store the sandwich in.
  * Kitchen Sink anti-pattern:  Start with the Workshop anti-pattern.  Take the giant hamper with you as you go about your day.  At random times during the day, work on preparing the sandwich.  At any given point, an external observer cannot know how close to completed the sandwich is.

Workshop Anti-Pattern:  Collating the set of things needed to do a particular thing into one module, and calling it an 'abstraction'.  This can be fine if the module has a clear purpose, and all components within it are cleanly separated.  But this is very bad if the component is just a bunch of very different things that are all tangled together.
  * An example of a failure to separate concerns, because one mistakenly things all the separate things are the _same_ concern.
  * Perhaps should put this Anti-pattern at the end of the section on Separation Of Concerns.

Kitchen Sink Anti-Pattern:  Using the Workshop anti-pattern, and carrying the heavyweight Workshop module around everywhere in your code, before finally using 'lazy evaluation' to get the actual result at the last possible moment.