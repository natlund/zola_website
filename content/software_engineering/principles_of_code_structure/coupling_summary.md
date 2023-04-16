+++
title = "Coupling Summary"
date = 2023-04-16
weight = 138
+++

## Summary

<table class="dense-table">
   <caption>Some Connections Between Software Modules</caption>
   <thead>
      <tr> <th><!--Blank--></th> <th>Simplicity</th>          <th>Replaceability</th> </tr>
   </thead>
   <tbody>
      <tr>
        <th>Function Call</th>
        <td>Simple as possible</td>
        <td><ul><li>New function</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Class Method Call</th>
        <td>Simple.<br>Class is namespace</td>
        <td><ul><li>New class or method</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Object Method Call</th>
        <td>Medium.<br>Overhead of instantiation</td>
        <td><ul><li>New class or method</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Injected Function Call</th>
        <td>Somewhat Complex.<br>Three modules, but each<br>module is simple</td>
        <td><ul><li>New function</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Injected Object<br>Method Call</th>
        <td>Complex.<br>Three modules.<br>Overhead of instantiation</td>
        <td><ul><li>New class</li><li>One-line change</li></ul></td>
      </tr>
      <tr>
        <th>Inheritance</th>
        <td>Complex.<br>Three modules.<br>Possible irrelevant<br>inherited connections</td>
        <td>Worst case:<ul><li>New parent class</li><li>Refactor class hierarchy</li><li>One-line change</li></ul></td>
     </tr>
   </tbody>
</table>


## Conclusions

Don't use inheritance.  Be _very_ careful with dependency injection.  Favour simple direct connections.
