+++
title = "Coupling Summary"
date = 2023-04-16
weight = 170
+++

# Summary

<table class="dense-table">
   <caption>Some Connections Between Software Modules</caption>
   <thead>
      <tr> <th><!--Blank--></th> <th>Simplicity</th>          <th>Replaceability</th> </tr>
   </thead>
   <tbody>
      <tr>
        <th>Function Call</th>
        <td><ul><li>Simple as possible</li><li>Coupling is simply Call</li></td>
        <td><ul><li>New function</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Class Method Call</th>
        <td><ul><li>Simple</li><li>Class is namespace</li><li>Coupling is simply Call</li></ul></td>
        <td><ul><li>New class or method</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Object Method Call</th>
        <td><ul><li>Medium</li><li>Two-part Coupling:<br>Instantiation + Call</li></ul></td>
        <td><ul><li>New class or method</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Injected Function Call</th>
        <td><ul><li>Somewhat Complex.</li><li>Three modules, but each<br>module is simple</li><li>Two-part Coupling:<br>Injection + Call,<br>in different parts of code</li></ul></td>
        <td><ul><li>New function</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Injected Object<br>Method Call</th>
        <td><ul><li>Complex</li><li>Three modules</li><li>Three-part Coupling:<br>Instantiation + Injection + Call,<br>Call in different part of code</li></ul></td>
        <td><ul><li>New class</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Inheritance</th>
        <td><ul><li>Complex</li><li>Three modules</li><li>Two-part Coupling:<br>Inheritance + Call</li><li>Possible irrelevant inherited connections</li></ul></td>
        <td>Worst case:<ul><li>New parent class</li><li>Refactor class hierarchy</li><li>One-line change</li></ul></td>
     </tr>
   </tbody>
</table>


## Conclusions

This little analysis shows that connections between software modules vary quite considerably in their complexity, and therefore in their readability.  Direct connections are considerably simpler than any form of dependency injection.  Inheritance may be fairly simple as far as it goes, but it may also drag along an arbitrarily large amount of 'collateral coupling' to things that are _not_ actually dependencies.

The obvious question is: Are there benefits to the more complex forms of connection?

In the limited scope of this preliminary analysis, the surprising answer seems to be 'no'.  We have defined a specific simple form of code modification, that we have called 'Replaceability', and discovered that achieving it is _equally easy_ for all forms of code connection, except inheritance:  For all connections except inheritance, swapping out a module simply requires writing the new module and changing _a single line_ of code.

Inheritance suffers from the fact that, in the worst case, the inheritance/abstraction hierarchy may be discovered to be wrong, and the entire inheritance hierarchy needs to be rewritten, just to swap out a module.  Or even worse, an ugly _workaround_ needs to be hacked into place, which will severely damage readability.  This fragility of inheritance appears to be well-understood in the Object-Oriented community nowadays.  The standard advice since at least the dawn of the 21st century has been to "favour object composition over inheritance".

Now, this little analysis of 'ease of code modification' has been restricted to 'ease of swapping out one module for a replacement'.  Of course, there may be _other_ reasons to favour a more complex connection such as dependency injection.  For example, ease of testing, or confining code changes to certain parts of the code base.  The lesson from this little analyis is that sometimes claims of 'extensible, modular code' turn out to be hollow.  When designing a software architecture, we want an accurate picture of the true costs and benefits of each design, so we can decide on the appropriate trade-offs.  It is not enough to blindly accept dogma.

A deeper analysis of connections is beyond the scope of this work.  But we can propose a few rules of thumb:
* Avoid inheritance, in general.
* Be _very_ careful with dependency injection.
* Favour simple direct connections.
* Connect a module if and only if it is a dependency.  (If it aint' a dependency, don't couple it.  If it _is_ a dependency, connect it as directly as possible.)

