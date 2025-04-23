+++
title = "Thinking Like An Engineer"
date = 2023-04-27
weight = 230
+++

# Thinking Like An Engineer

## Format Code Perfectly At All Times

Keep code formatting perfect at all times.  _Don't_ say to yourself "I'll come back and fix the formatting later."  Write your code in the same way that a professional chef would practise 'clean as you go' in a busy commercial kitchen.  This discipline helps instil both the attention to detail and sensitivity to structure that characterise a good engineering mind.

## Be Explicit

When reviewing computer code or working with another engineer, the phrase I find myself using the most often is "Be Explicit", and variations thereof.  Let me as the reader know _exactly_ what I need to know to understand what is going on.  Don't make me guess - crush ambiguity.  Express Intent: tell the reader what the code is trying to achieve.

The corollary to this is to hide away stuff that isn't important - don't distract me with irrelevance.  Take great care in deciding what is _really_ important to understanding the algorithm, and bring it to the surface where the reader can see it.  So this principle circles back to the Art Of Abstraction first encountered at the beginning of this book.  The right abstractions (at the right level of abstraction) make your code _make sense_.  Therefore, carefully cultivate the skills of abstraction.

## Single Source Of Truth For Everything, Not Just Software

A foundational early chapter in this book was [_Single Source Of Truth_](@/software_engineering/principles_of_code_structure/single_source_of_truth.md), which introduced a concept of utmost importance for engineering successful code bases.

The philosophy of having a Single Source Of Truth applies far beyond just computer software.  Documentation, in particular, should be written with the philosophy in mind: things should be defined in one place.  More generally, all written materials should have a single source of truth.  Management and organisation structure benefit from having clear roles and responsibilities, with explicit boundaries on authority.  An engineer cannot serve two masters...  (Your author once served _five_ masters at the same time.)
