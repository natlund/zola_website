+++
title = "Outline Plans"
date = 2023-09-10
weight = 1
draft = false
+++


# Version 1, 2023-09-10

Chapters
1. Introduction
2. What Is Management?
3. 

## Introduction
These essays cover either engineering management practices that are proven to work through practical experience, or defensible ideas and frameworks that help in understanding engineering management.
* Written by an actual professional engineer who has worked with various engineering management methodologies, some good, most bad.
* Advice is based on concrete evidence of what actually works.
* Hence the choice of name '_Empirical_ Engineering Management'.

## What Is Management?

Careful reflection will reveal that a handful of activities and concerns constitute 'management'.
1. Process Setup.  Define processes.  Find metrics to measure them, that won't be gamed.  Refine continuously.
2. Process Tracking.  Ensure that processes are actually being followed. Box ticking (in a good way).
3. Project Initiation.  Create projects, define their purpose, assemble a team, start defining requirements and desired outcomes.
4. Project Tracking.  Ensure that all tasks in the project are actually getting done.

And two higher-level concerns:

5) People.  Manage people in the team, keeping them happy, productive, and progressing in their career.
6) Prioritisation.  Prioritise the projects (and processes).

Plus two more 'meta' concerns that often apply:

7. Vision.  Have a comprehensive vision of where the team is going, the long-term goal that the various projects are working towards.
8. Reporting.  Summarise the state of all processes and projects to higher management, and  other stakeholders.

Often, only one of Vision or Reporting will be needed.  If Vision is set by upper management, then it won't be part of the Team's remit, but Reporting will likely be necessary.  And vice versa: if a Team is fully responsible for its Vision, then it is less likely to be accountabe to higher powers via Reporting.

Question:  is Accountability a separate thing, or just part of Reporting?  I think it is just part of Reporting.

### Types of Management

1. Operations Management.  Managing work that is largely process-driven, repeatable work.
2. New Stuff Management.  Managing work that is largely project-based, about building new stuff.
4. Vision and Strategy Management?  Managing the process of figuring out what the company or product should look like in the future, and what needs to be built to get there.

Operations Management is the thing that keeps the business in business.  Though it is the least 'sexy' thing to manage, its value should not be underestimated.

New Stuff Management gets stuff built to expand the business offering (or indeed set it up to begin with).  It is difficult, and also can be objectively judged - did stuff get built or not?  Engineering Management falls in this category, which is the focus of this book.

Vision/Strategy Management is the highest-status form of management, because in _principle_ it determines the ultimate success of the company.  The wisdom to figure out _what_ to build requires insight gained from a lot of experience, and deep thought about the structure of the entire industry, and indeed the entire economy.  Unfortunately, the success of Strategy is notoriously difficult to objectively judge.  Thus, in _practice_, this level of management is infested with supremely confident bullshit-artists, who have honed the skill of _appearing_ to know what they are doing.  Dealing with this problem is beyond the scope of this book, but we shall offer the following advice: If a manager is not _excellent_ at Engineering Management, they almost certainly lack the rigour of thought to be a good strategist.  And don't hire smug extroverts in yellow hats.

## Planning

There are two fundamental truths about managing anything non-trivial:
1. **Planning Is Essential**.  It you fail to plan, you plan to fail.
2. **Plans Change**.  No plan survives first contact with reality.

There is a tension between these two facts.  All kinds of machinations, evasions, distortions, and convolutions have arisen to avoid dealing with the apparent contradiction between these two axioms.

We offer the best known way to handle these two truths:  Iterative Planning with Versioned Plans.

### Iterative Planning

1. Write the first version of the Project Plan.  The Plan should not be fully complete:  It should be accurate and complete for the first stages, then progressively more vague for tasks further into the future.  Stop writing the Plan once you have hit the point of diminishing returns.
2. Get on with the work.  You will learn many things, and discover many things that need to be decided.
3. After two weeks, create a new Version of the Plan.  Tick off all the things that were done, add in new things that were discovered, and revise the timeline for remaining work.
4. Repeat Steps 3 and 4.


### Four Kinds Of Documentation

1. Plans.  These are explicitly versioned, with a new version created every two weeks.
2. Background Material.  Largely created at the start of the project, and added to when needed.
3. Discussion. Grows without limit during the life of the project.  Added to constantly, daily if needed.
4. Specifications.  The digested results of Discussion. Revised and updated as soon as decisions are made.  But generally NOT versioned - old Specs are confusing, and the current Specs should always be up-to-date.

### Three Kinds Of Meeting

1. Broadcast.  A small subset of attendees talk, while everyone else listens.  Efficient way of transmitting information to a lot of people.
3. Reverse Broadcast.  Every one talks in turn, and only a small subset needs to hear what every one said.  Horribly inefficient for everybody except the manager who gets all updates in one go.
3. Discussion.  Most attendees talk.  If the group is as small as possible, this is the best way to solve problems.


### Management In The Absence Of Plans

If management are too incompetent to know the importance of writing plans (and iterating on them), then everybody muddles through in a state of partially self-organized chaos.  The first thing that happens is:

#### Management By Multitudinous Messages

People who are accountable for the outcome of the project will feel compelled to get the people who can do the work to actually do the work.  So they will send requests to start work.  The workers may respond with questions about the exact requirements.  This may require input from still other people.  More messages will be flung around, sometimes visible to all three parties, and sometimes only visible to two parties at a time.  Thus, there will four channels of messages: A and B and C, A and B only,  B and C only, A and C only.  The critical decisions and defined requirements will be scattered across all four channels.

In practice, it is even worse.  If there are more than three parties required for the project, then the proliferation of channels grows.  In fact, if there are N people in the project, the number of possible channels is the number of possible subsets of a set of size N, which is 2^N.

Eventually, with key information hidden away on various emails, Slack messages, and threads, things fall through the cracks, and things don't get done.  If this gets so bad that the incompetent management actually notice, they will 'take charge of the situation', and attempt: 

#### Management By Massive Meeting

Inefficient waste of time that lazy, incompetent managers do to appear to be 'taking charge'.
The type of incompetent managers who call massive meetings almost **never** do the right thing, which is to find someone intelligent to _write stuff down_, that is, _make a fucking plan._