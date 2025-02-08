# Software Design Heuristics

These are the heuristics I find useful in my software engineering practice.
I use the term "heuristics" to describe anything that helps me write better code, as long as I keep them in mind.

Some heuristics are my own, while others come from great books.
Heuristics cited here always include references to their sources.

All of these heuristics are effective only when considered together. Taken in isolation, some may even contradict one another: if you focus on just a few and apply them too rigidly, they may lose their value or even lead to negative outcomes. Some heuristics may overlap with others, so don't take them too seriously.

This is currently just a draft—far from complete, with random notes organized arbitrarily. Please don't expect it to be polished.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [General](#general)
  - [Fast Feedback](#fast-feedback)
  - [Start Simple](#start-simple)
  - [Habitability](#habitability)
  - [Prima Materia](#prima-materia)
  - [Crash Early](#crash-early)
  - [Poisonous Systems](#poisonous-systems)
  - [Bad Design in House](#bad-design-in-house)
  - [Good Will vs Pain](#good-will-vs-pain)
  - [Code Style as a Blocker](#code-style-as-a-blocker)
  - [Masking (Shadowing)](#masking-shadowing)
  - [Code that Works](#code-that-works)
  - [Code is Not Your Partner](#code-is-not-your-partner)
  - [Refactoring I](#refactoring-i)
  - [Everything is Scope, Scope is Everything](#everything-is-scope-scope-is-everything)
  - [Everything Explicit. No Magic.](#everything-explicit-no-magic)
  - ["Magic" is automation that is not adequate](#magic-is-automation-that-is-not-adequate)
  - [Fast Programming and Slow Programming](#fast-programming-and-slow-programming)
  - [Quick exploration](#quick-exploration)
  - [Other](#other)
- [Complexity and Cognitive Load](#complexity-and-cognitive-load)
  - [Black Box with a Green Play Button](#black-box-with-a-green-play-button)
  - [Humans are not designed for Big Numbers](#humans-are-not-designed-for-big-numbers)
  - [Weakest link](#weakest-link)
  - [There is no such thing as Many](#there-is-no-such-thing-as-many)
  - [0-1-2-Many I](#0-1-2-many-i)
  - [0-1-2-Many II](#0-1-2-many-ii)
  - [Periphery](#periphery)
  - [Solving Right Problems](#solving-right-problems)
  - [Solutions are Context-Driven](#solutions-are-context-driven)
  - [Solving Problems with Cash](#solving-problems-with-cash)
  - [Rational and Unconscious](#rational-and-unconscious)
  - [Point of View](#point-of-view)
- [Design](#design)
  - [Poor Abstraction](#poor-abstraction)
  - [Hard Feature](#hard-feature)
  - [True Name](#true-name)
  - [One Pattern per Class](#one-pattern-per-class)
  - [Archetype](#archetype)
  - [Trade-off of Encapsulation](#trade-off-of-encapsulation)
  - [Unnecessary Flexibility](#unnecessary-flexibility)
  - [Single Source Concept and Its Exceptions](#single-source-concept-and-its-exceptions)
  - [Resilience to Change vs Fixed Perfect Solutions](#resilience-to-change-vs-fixed-perfect-solutions)
  - [Two Almost Identical Entities](#two-almost-identical-entities)
  - [Control](#control)
    - [Observable Control](#observable-control)
    - [Humans should dominate machines](#humans-should-dominate-machines)
    - [Overlapping control](#overlapping-control)
    - [Broken control loops](#broken-control-loops)
  - [Feedback](#feedback)
    - [Broken feedback loops](#broken-feedback-loops)
  - [Separation / partitioning](#separation--partitioning)
  - [Grouping](#grouping)
  - [Observability vs Correctness](#observability-vs-correctness)
  - [Don't Use RAII on a Business Logic Level](#dont-use-raii-on-a-business-logic-level)
- [Day-to-day work](#day-to-day-work)
  - [Leave Work Better: Improving Today for a Simpler Tomorrow](#leave-work-better-improving-today-for-a-simpler-tomorrow)
  - [Task Sequencing: Group Related Activities for Efficiency](#task-sequencing-group-related-activities-for-efficiency)
- [Coding and code reviews](#coding-and-code-reviews)
  - [The Moving and Changing Anti-pattern](#the-moving-and-changing-anti-pattern)
- [Maintenance Programming](#maintenance-programming)
  - [Stable Components](#stable-components)
  - [Boring Code](#boring-code)
  - [Boring Code 2](#boring-code-2)
  - [Lack of Knowledge](#lack-of-knowledge)
  - [Lack of Knowledge II](#lack-of-knowledge-ii)
- [Testing](#testing)
- [Distribution](#distribution)
  - [Provide Basic Test Sequences with Your Product](#provide-basic-test-sequences-with-your-product)
  - [Provide Drivers Alongside Your Hardware](#provide-drivers-alongside-your-hardware)
- [Reliability](#reliability)
  - [Errors are not ok](#errors-are-not-ok)
  - [Errors must be understood and described](#errors-must-be-understood-and-described)
  - [Underlying errors shall not be hidden](#underlying-errors-shall-not-be-hidden)
  - [Critical errors vs non-critical errors](#critical-errors-vs-non-critical-errors)
  - [Assertions are better than no error handling](#assertions-are-better-than-no-error-handling)
  - [Assertions are shortcuts for a proper error handling](#assertions-are-shortcuts-for-a-proper-error-handling)
- [Systems](#systems)
  - [Good enough is often best](#good-enough-is-often-best)
  - [Designing Systems for Effective Work](#designing-systems-for-effective-work)
- [People and Organizations](#people-and-organizations)
  - [Everyone is busy](#everyone-is-busy)
  - [Four seasons](#four-seasons)
- [Meetings](#meetings)
  - [Sound Check](#sound-check)
  - [Meeting Agenda](#meeting-agenda)
  - [Meeting Notes](#meeting-notes)
  - [Capturing Meeting Results](#capturing-meeting-results)
  - [Briefing In](#briefing-in)
  - [Sharing Screen & Presenting Material](#sharing-screen--presenting-material)
- [Biases](#biases)
  - [The Working-So-It's-Right Bias](#the-working-so-its-right-bias)
  - [The Fix Bias](#the-fix-bias)
  - [Resolving Merge Conflict Bias](#resolving-merge-conflict-bias)
- [Documentation](#documentation)
  - [Less prose, more structure](#less-prose-more-structure)
  - [Too Much Structure Overload](#too-much-structure-overload)
  - [Encyclopedic Document](#encyclopedic-document)
- [Standards](#standards)
  - [Idealized standards vs. practical implementation](#idealized-standards-vs-practical-implementation)
  - [The challenge of standards implementation](#the-challenge-of-standards-implementation)
  - [Standards and best practices](#standards-and-best-practices)
  - [Standards favor good practice](#standards-favor-good-practice)
  - [Wrong is worse than early or incomplete](#wrong-is-worse-than-early-or-incomplete)
- [Requirements](#requirements)
  - [One-stop shopping](#one-stop-shopping)
- [Safety](#safety)
  - [Safety does not exist without blood, loss or failure](#safety-does-not-exist-without-blood-loss-or-failure)
  - [Safety is boring](#safety-is-boring)
  - [Safety is very hard to achieve but is very easy to lose](#safety-is-very-hard-to-achieve-but-is-very-easy-to-lose)
  - [Success breeds failure](#success-breeds-failure)
  - [Safety as a Defensive Discipline](#safety-as-a-defensive-discipline)
  - [Safety for Engineering is Like Medicine for People](#safety-for-engineering-is-like-medicine-for-people)
  - [User Interfaces and Critical Systems](#user-interfaces-and-critical-systems)
- [Books](#books)
- [Similar resources](#similar-resources)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## General

### Fast Feedback

Getting feedback fast is essential for an engineer. The two great ways of
getting feedback fast are test-driven development and debugging techniques.
When you come to a new project, first of all learn how to run existing and write
new tests and also learn how can you debug things the fastest way (can be a real
debugger, or just "console.log()").

### Start Simple

Start with something simple, then extend it further. Most often a complex
problem is a composition of simpler problems. If you are facing a problem and
you are afraid of the complexity it exerts, try to make a smallest possible step
towards the solution and see what you can do from there. Simple can also mean
quick and dirty but that's ok as that's only a start. Once you have something
simple working you have a ground to move on further. Most likely this means you
have an **archetype** of a future thing, real and complex system.

See also Kent Beck's
[Test-Driven Development book](https://en.wikipedia.org/wiki/Test-Driven_Development_by_Example)
where this approach of doing simple things is explained at great depth.

### Habitability

Habitable software is better than perfect software.

[Richard Gabriel - Patterns of Software, Habitability and Piecemeal Growth](https://www.dreamsongs.com/Files/PatternsOfSoftware.pdf).

> Habitability is the characteristic of source code that enables programmers,
coders, bug-fixers, and people coming to the code later in its life to understand its
construction and intentions and to change it comfortably and confidently. Either
there is more to habitability than clarity or the two characteristics are different...

> ...Habitability makes a place livable, like home. And this is what we want in
software — that developers feel at home, can place their hands on any item without
having to think deeply about where it is. It's something like clarity, but clarity is
too hard to come by.

### Prima Materia

Sometimes to make further progress you need to un-implement (break!) particular
pattern/architecture/solution and put it back into
[Prima Materia](https://en.wikipedia.org/wiki/Prima_materia) state and only then
thansform it into a something new. Metaphors similar to Prima Materia are
"primordial soup" and "indifferentiated soup of ideas" (Eric Evans - DDD).

### Crash Early

If you know how to not program defensively in a particular situation go ahead!
Otherwise make your code to Crash Early to catch bugs as early as possible: use
sensible assertions and stress edge-cases with tests. See
[Some notes C in 2016: Code offensively](http://blog.erratasec.com/2016/01/some-notes-c-in-2016.html#.VtGEKBg7T5c)
and
[Spotify engineering culture (part 2): "We aim to mistakes faster than anyone else"](https://labs.spotify.com/2014/09/20/spotify-engineering-culture-part-2/).

### Poisonous Systems

Badly designed systems tend to poison systems they interact with.

### Bad Design in House

Do not overdesign your own software if you have a big producer of bad or
too opinionated designs nearby. A big producer can be a vendor or a team
with authority who decided to rely on a given design a while ago.

### Good Will vs Pain

Lots of what we programmers learn with years comes from pain, not from good will.

### Code Style as a Blocker

Sometimes code style can be a blocker. Poorly formatted code can make
understanding of it extremely difficult. Do everything to reduce your cognitive
load. Real-world example:

```swift
let expectedRemainingLoops = Int(ceil( (expectedRemainingElements - Double(currentRemainingElementsForLoop)) / Double(PPENumberOfTasksInCurrentLoop) ))
```

reads much better if

```swift
let expectedRemainingLoops =
  Int(
    ceil(
      (expectedRemainingElements - Double(currentRemainingElementsForLoop)) /
      Double(PPENumberOfTasksInCurrentLoop)
    )
  )
```

### Masking (Shadowing)

Masking/shadowing of all kinds is dangerous and should be avoided or treated
with a great care.

Examples:

- errors introduced to the systems when overlapping requirements are implemented
over time
- masking in MC/DC
- shadowing of variable declarations
- typographically ambiguous symbols with overlapping visibility like `l` and
`1`, `O` and `0` (see MISRA guidelines)
- code reviews: real bugs can hide behind less important but more noticeable
issues like typos or coding style details
- bugs often hide themselves behind complexity

See also Overlapping Control.

### Code that Works

Working code with a good enough architecture is better than buggy code with
a perfect architecture.

### Code is Not Your Partner

Sometimes we don't have to be nice about other people's code:

  - can be different platforms
  - can be outdated code
  - can be ancient build tools
  - can be the code that has some parts you don't need
  - can be mistakes

In this case it is fine to delete or agressively modify some code to compile it, test it, learn about it.

### Refactoring I

Replace != "Remove + Write". Replace = "Write new + Re-route + Remove old".

### Everything is Scope, Scope is Everything

- Restrict the scope of data to the smallest possible. (The Power of 10: Rules
for Developing Safety-Critical Code by NASA)

### Everything Explicit. No Magic.

Whenever a thought explicit vs magic comes to your mind, go for explicit.

### "Magic" is automation that is not adequate

In the beginning, there is no magic, but simply a desire to automate things to
reduce repetition. Magic appears as a result of increasing complexity that makes
current solution to be inadequate for further progress. Magic can also emerge
rather quickly as a result of automating wrong things from the beginning.
The holy grail is automation that is always adequate.

### Fast Programming and Slow Programming

This can be read as prototype vs maintenance programming. Fast Programming is
essential for a quick progress and is very much encouraged by the business.
However it rarely does have time to learn from mistakes due to the effect of
the tunnel, "straight ahead", way of thinking. Slow Programming has a virtue of
reflection and deeper analysis but is probably too slow to get the business
going from scratch. Business starts to appreciate Slow Programming only when it
hits the wall of complexity and therefore the need in a proper design.

### Quick exploration

It is not unusual that the solution you are looking for may be in two clicks and couple of Google search results away from you. When reading large documents, sometimes it is useful to "fly over" a document to find a section that is most releveant, instead of reading through the document A-to-Z.

### Other

- Don't give your classes plural names. See also "There is no such thing
as Many".

## Complexity and Cognitive Load

> "Complexity can be defined as intellectual unmanageability"
(Nancy Leveson, Engineering a Safer World, p.4)

https://en.wikipedia.org/wiki/Cognitive_load (and Cognitive Overload)

### Black Box with a Green Play Button

Ideal interface for a system of arbitrary complexity is a black box with a green
play button on it - you take the box, press green button and it just works. The
second ideal interface is when you also have a red button to stop the system.

### Humans are not designed for Big Numbers

If you have to work with something that involves a big number of entities, like
do something on 10000 files or work with megabytes of data, start with reducing
this quantity to a minimum possible number of entities so that still makes sense
for a prototype of your final work: make it work with 1 file instead of 10000 or
with 20 bytes instead of 20 gigabytes.

### Weakest link

A piece of information is only as clear as its most ambiguous piece. This is a
generalisation from the following fragment from "Patterns for Writing
Effective Use Cases" by Steve Adolph et al., Chapter 6.6:

> Like the old proverb, "A chain is only as strong as its weakest link", a use
case is only as clear as its most ambiguous step.

### There is no such thing as Many

Many does exist but it is difficult to cognize with a human mind. Many needs an
Umbrella, that turns it into One in the way we think about it. Many can be
homogenous like Array of objects of the same type or heterogeneous, for example
a bunch of instructions in the code or multiple functions in a test class or a
set of User Profile fields of various types: name (string), age (int), settings
(object). Collections are easier because they hide Many from us behind a
well-defined interface: `containsObject`, `getAtIndex`, `enumerateWithIndex`,
which saves us from dealing with Many directly. Heterogeneous Many is harder:
you have to cognize and organize it yourself: group instructions into meaningful
functions, group fields into meaningful containers like structs or database
tables.

One programming construct that fails to constrain Many is tuple: you start doing
things like `let person = ("John", 32)` and `let (name, age) = person` or things
like `person.1` but then you quickly find yourself in a mess when the number
grows to a real Many (quick lesson: don't use tuples, use structs!). If you have
Many, find a way to think and work with it like One.

### 0-1-2-Many I

Most of the people start saying "so many", "infinite" when there is actually 3
or 4, rarely more, things on the table. Variation is 1a, 1b, 2a, 2b which is
still within limit of 3 or 4. This looks like ancient calculator: when 0, 1, 2
and then 'many'. Algebra looks fairly simple: 0 + 1 = 1, 1 + 1 = 2,
2 + 1 = many, 2 + 2 = many, etc. Consequence: people are quite susceptible to
small numbers. Say something like "this consists of 3 steps" and people will get
it. Don't say "seven". See also **Humans are not designed for Big Numbers**.

### 0-1-2-Many II

Don't start to abstract or DRY from just two things. Wait until you have at
least 3 of them. See also **Duplication is better than poor abstraction**.

### Periphery

If your reasoning is complicated by cognitive overload that you have after a
problem you are trying to solve and there is no obvious way to make a first step
towards solution, take a step back and start working with Periphery. Good
example is legacy code: poor periphery like bad variable names, wrong
responsibilities in classes, even those who are distant to your problem, bad
folder structure, etc might look completely irrelevant to the core of your
problem but still it contributes to the cognitive overload - try to clean up
periphery and you will see that the core of your problem is now more clear and
approachable than it was before. Another word for Periphery is Background, see
also [Deconcentation of Attention](http://deconcentration-of-attention.com/).

### Solving Right Problems

"Engineers are great at solving problems but they are not always great at
identifying the right problems to be solved"
(Dr. John Thomas, ESWC 2019).

### Solutions are Context-Driven

Even the best solution to a problem is valid only within a given context. A slight change in the context can invalidate the solution, requiring one to start from scratch. This understanding highlights that no solution is universally perfect. Instead, solutions address specific problems or contexts in an "optimal enough" way. It also encourages detachment from ego-driven perfection, allowing solutions to evolve as the environment changes.

Examples:

- A clean architecture or pattern may shift to a completely different, sometimes opposite, solution due to changing requirements or system environments.
- A "perfect" solution might be discarded because a new team or team leader dislikes technology X and prefers technology Y, or simply because it aligns with emerging industry trends.
- Perfectly clean code may be rewritten and become more obfuscated due to necessary performance optimizations.
- Highly efficient code might be rewritten to sacrifice performance in favor of better maintainability and readability, especially for a larger team.

### Solving Problems with Cash

Every engineering problem can be solved with an infinite amount of cash.

### Rational and Unconscious

Engineers create rational artifacts, which may appear simple and mundane. 
However, the process behind their creation often involves deep reflection 
and can stem from the unconscious mind.

### Point of View

[How NASA Builds Teams](https://www.wiley.com/en-us/How+NASA+Builds+Teams%3A+Mission+Critical+Soft+Skills+for+Scientists%2C+Engineers%2C+and+Project+Teams-p-9780470456484):

> The right coordinate system can turn an impossible problem into two really 
> hard ones.

[The Early History Of Smalltalk](https://worrydream.com/EarlyHistoryOfSmalltalk/)

> Watching a famous guy much smarter than I struggle for more than 30 minutes 
to not quite solve the problem his way (there was a bug) made quite an 
> impression. It brought home to me once again that "point of view is worth 
> 80 IQ points." I wasn't smarter but I had a much better internal thinking 
> tool to amplify my abilities. This incident and others like it made 
> paramount that any tool for children should have great thinking patterns 
> and deep beauty "built-in."

## Design

### Poor Abstraction

> Duplication is better than poor abstraction (Sandi Metz, Rails Club 2014, Moscow).

> "...ill-fitting structure is worse than none..." (Eric Evans - Domain-Driven Design, p.446)

A good example from https://www.sigbus.info/worse-is-better:

> In lld v2, we decided not to use an intermediate representation. Instead, 
> we directly handle platform-dependent native file formats. lld v2 consists 
> of virtually three different linkers for Windows, macOS and Unix. They 
> share the same design but do not share code. Naturally, we sometimes had 
> to write very similar code for each target. This may seem like an 
> amateur-level programming mistake, but in reality, it's much easier to 
> write straightforward code for each target than writing unified one that 
> covers all the details and corner cases of all supported targets 
> simultaneously. 

### Hard Feature

If a feature is hard to implement it might indicate that it is something wrong
with the feature (or product).

### True Name

If you know [True Name](https://en.wikipedia.org/wiki/True_name) of something
you have power over it. Good class name - this is what True Name is in OOP.

> "A well-chosen word can save an enormous amount of thought",
(said by Mach according to S.R.Cajal, Santiago Ramón y Cajal,
"Advice for a young investigator")

See also
[Mass and Gravity](http://www.carlopescio.com/2008/12/notes-on-software-design-chapter-2-mass.html).

### One Pattern per Class

A class violates Single Responsibility Principle if it contains implementation
of more than one design pattern. Of course there are exceptions.

### Archetype

Archetype is an umbrella concept for other concepts like: `prototype`,
`proof of concept`, `minimal viable product`. Archetype means something simple
and coherent. If you know the archetype of something you understand the essence
of it. A complex system can be traced back to a one or a number of underlying
archetypes.

Interesting side note: as far as I see it, the tendency is that engineers as
they grow their software bigger, do not care much about the underlying
archetypes. Imagine how easy it would be to learn about the software if it would
contain itself in its earliest forms of being (source code, documentation,
drafts etc). Great example: Rust programming language had to start from
[somewhere](https://github.com/graydon/rust-prehistory).

> "View the problem in its simplest forms ... An excellent method for determining
the meaning of something is to find out how it comes to be what it is."
(Santiago Ramón y Cajal, "Advice for a young investigator")

### Trade-off of Encapsulation

Strong, "tight", encapsulation is good but don't forget about the users:
Operations people. Good example is debugging facilities - if you close
everything then you leave the ops people, who might be you, without any tools to
understand or tweak your system. Richard Cook explains this very well:
See [Velocity 2012: Richard Cook, "How Complex Systems Fail"](https://www.youtube.com/watch?v=2S0k12uZR14).

### Unnecessary Flexibility

(from [Writing Solid Code](http://writingsolidcode.com/))

> Flexibility breeds bugs. Another strategy you can use to prevent bugs is to
strip unnecessary flexibility from your designs... The trouble with flexible
designs is that the more flexible they are, the harder it is to detect bugs.

> ...Flexible features are troublesome because they can lead to unexpected
"legal" situations that you didn't think to test for even realize were legal...

> ...When you implement features in your own projects, make them easy to use;
don't make them unnecessary flexible. There is a difference.
Don't allow unnecessary flexibility.

### Single Source Concept and Its Exceptions

The Single Source (of Truth) concept is one of the first principles beginner 
programmers learn and often becomes a rule they follow rigorously. However, 
like many principles in life, it has its exceptions. Blindly adhering to the 
Single Source rule can sometimes lead to suboptimal results.

A good example of when this principle might fail is the
[Poor Abstraction](#poor-abstraction) 
scenario. This happens when someone tries to consolidate similar elements 
into a single source while ignoring their significant differences. In such 
cases, forcing everything into one place can create an abstraction that is 
brittle, confusing, or overly complex, ultimately making the system harder 
to understand and maintain.

Another example is
[Two Almost Identical Entities](#two-almost-identical-entities).
This occurs when someone tries to merge two seemingly identical entities 
into one, which results in an overly complicated "Single Source of Truth" 
codebase. This approach often leads to significant branching logic and 
reduced readability, making the code harder to work with and more prone to 
errors.

Understanding when to apply the Single Source principle and when to allow 
for exceptions—is crucial for achieving balance and maintaining flexibility 
in software design. Learning where to follow and where to de-prioritize the 
Single Source principle is a good skill that distinguishes a more 
experienced programmer from a beginner one.

### Resilience to Change vs Fixed Perfect Solutions

When designing a system, there is a trade-off between making it easier to 
change in the future and striving for perfection. In most cases, choosing 
flexibility is the better option. If you anticipate changes in context or 
additional development work that could affect the system, avoid focusing too 
much on perfecting the existing solution, as it may not hold up under new 
pressures. Another important consideration is the ability to undo or disable 
a function that works perfectly now but could cause unforeseen issues in 
operation. Often, a perfectly working solution can create obstacles for 
other systems or people involved in operating the system.

### Two Almost Identical Entities

Over the years I have seen at least three big units of a hardly manageable
legacy code where each of them was built on two almost identical entities. There
are two ways of such things to co-exist:

1. One is a subclass of the other.
2. Two almost identical hierarchies are maintained.
3. Two groups of helper functions without a clear separatation of
responsibilities between them.

It seems that historically in all three cases it started with one entity that
accumulated its features along the way, then came the other which was so
similar to the first that programmer avoided extraction of similar modules that
both entities had and went with subclassing to get the result quickly or with 2
parallel hierarchies.

To these days I still didn't see or create an elegant solution to this problem.
See also "Hard Feature".

### Control

One of the key concerns is Control: where control should or should not be,
what should have control (be active) and what should not have (passive).

#### Observable Control

Software should be designed in such a way that there always should be a dedicated
place where it is obvious how the control and work flow through the software.
This should be effective on all levels of abstraction and for each level of
abstraction, such dedicated software should be free of the lower-level
implementation details that discourage easy understanding of context.

If something creates a low-level implementation noise on a given level,
it might be a good sign that one or more underlying lower layers exist where
that lower-level implementation can be represented as a high-level workflow
logic (sequence of steps or algorithm).

#### Humans should dominate machines

The lower-level modules should not have control over higher-level modules.
It is not only about not having higher-level module imported in lower-level
modules and making everything to work through protocols/interfaces but more
about what is the flow of control: "what controls what". Two shortcuts:
**humans should dominate machines**, **business logic should dominate the
system's implementation details**.

#### Overlapping control

Overlapping things is a challenge for a human mind and therefore is bad for the
whole software lifecycle: design, development, testing and maintenance. This
might be two or more classes that do the same thing. This might be two or more
people whose responsibilities overlap. Nancy Leveson says Overlapping Control
is one of the greatest sources of safety problems: two controllers whose areas
of responsibilities overlap (see "Engineering a Safer World"). See also "Two
almost identical entities" and "Shadowing/Masking".

#### Broken control loops

The top-level controllers should always have a control over the bottom-level
elements. If the controllers include both humans and automation, the humans
should always be able to intervene and take over the control provided by the
automation.

This heuristic can be turned into explicit design constraint.

### Feedback

#### Broken feedback loops

Missing, insufficient or incorrect feedback is a great source of troubles for
any system.

"All feedback loops must be closed" - this heuristic can be turned into
explicit design constraint.

### Separation / partitioning

- Separate stable from unstable
- Separate permanent from temporary
- Separate synchronous from asynchronous
- Separate similar from different
- Separate symmetrical from asymmetrical
- Balance and symmetry: if one partition has way more items than the other
  ones, this may indicate that the partitioning has not been complete.
- Separate construction from operation (one example: Factory vs Command)
- Separate content from presentation (applies to UI-heavy code, great example: HTML/CSS)
- Separate easy from complex: isolate easy, isolate complex, repeat many times
- Separate stateless from stateful
- Separate data from behavior and behavior from data unless you do have a good
OOP class/object with good data/behavior balance.
- Separate general-purpose from application-specific
- Separate application-level code from system-level code
- Separate methods that read from methods that write
- Separate decision from condition
- Separate One from Many, separate Many from Many.

Example 1: "Monolithic test case files"

In the following example the `_feature1_` or `_feature2_` parts and numbers in
the test method names assist a lot in logical grouping of the tested
functionality.

```c
# Many group #1
test_feature1_1() {}
test_feature1_2() {}
test_feature1_3() {}
# Many group #2
test_feature2_1() {}
test_feature2_2() {}
test_feature2_3() {}
```

Example 2: the inner block has a multiline routine which could actually be another function that works on one. At the same time this inner block on many. Unless we create that another function we have a conflict between many of the enumeration and many of the instructions inside a block.

```cpp
EnumerateInstructions(*function, [&](Instruction &instr, int bbIndex, int iIndex)
{
  ... lots of lines working on `instr` ...
});
```

### Grouping

- Group together things that change at the same time. If possible create container
data structures so that a change involves a change of **one**. If possible,
group all the changes that happen at the same time together.

- Group things that are used together.

### Observability vs Correctness

Incorrect but observable code can be more valuable long-term than correct 
but unobservable code. Observable code is easier to inspect, test, and 
improve, even if it contains mistakes. In contrast, correct but hidden code 
can become difficult to maintain and debug over time, creating technical 
debt. Visibility allows for quicker fixes and ongoing improvement, making it 
more sustainable in the long run.

### Don't Use RAII on a Business Logic Level

RAII is good for resource management, such as handling memory, file 
handles, or network connections, where resources need predictable 
acquisition and release. However, applying RAII to business logic can lead 
to significant problems:

- Reduced flexibility: RAII assumes that actions are tied directly to scope, 
  but business workflows may need to defer, combine, or otherwise manage 
  actions independently of object lifetimes.

- Lack of transaction control: Business operations often involve external 
  systems, validation, or rollback mechanisms that require precise control. 
  RAII hides these processes behind object lifecycle management, making it 
  harder to handle errors or maintain consistency.

- Unintended side effects: Business logic often involves workflows with 
  complex rules and dependencies. Tying actions like adding or removing data 
  to the lifecycle of objects can cause unexpected behaviors if those 
  objects are destroyed prematurely or unintentionally.

- Debugging challenges: When business actions are implicitly triggered by 
  object lifetimes, it becomes harder to trace when and why specific 
  operations occur. This lack of clarity can lead to subtle bugs that are 
  difficult to identify and fix.

Instead of using RAII, manage business logic explicitly through well-defined 
methods or services. This approach keeps the logic transparent, easier to 
understand, and more adaptable to changing requirements.

## Day-to-day work

### Leave Work Better: Improving Today for a Simpler Tomorrow

Always leave the work artifacts—whether code, documentation, diagrams, models, or others—in a better state than they were before, giving future you or someone else the opportunity to improve them even further.

### Task Sequencing: Group Related Activities for Efficiency

When sequencing tasks (especially repetitive ones), group related tasks together and separate them from others.

One useful pattern is the 'Inbox' approach, where input is first collected and then executed upon. For example, when writing a technical document, split the task of gathering the document content (the 'Inbox' with bullet points) from the task of formulating and spelling out each individual content item.

## Coding and code reviews

### The Moving and Changing Anti-pattern

A great anti-pattern that complicates code reviews is creating a changeset 
that involves both moving and changing things at the same time. This 
obscures the diffs in the version control system, making it harder to track 
changes. The solution: isolate moving and changing into separate commits or 
separate PRs.

## Maintenance Programming

### Stable Components

Stable Components is a resort of a Maintenance Programmer. One way for a
developer to survive in a large legacy project is to create stable components or
extract them out of existing mess of code. Stable component most likely means a
testable component: it can be a parsing module or API layer or string
manipulation helpers. Having such islands of stability helps a lot to overcome
the difficulties of a maintenance programming. See also Periphery and Prima
Materia Heuristics.

### Boring Code

(from [Writing Solid Code](http://writingsolidcode.com/))

> If your code feels tricky, that's your gut telling you that something isn't right. Listen to your gut. If you find yourself
thinking of a piece of code as a near trick, you're really saying to yourself that an algorithm produces correct results even though it is not apparent that it should. The bugs won't be apparent to you either.

> Be truly clever; write boring code. You'll have fewer bugs, and the maintenance programmers will love you for it.

### Boring Code 2

Complex software is not to be developed and used by average programmers. This
happens anyway because of production pressures. People say: your mileage may
vary.

### Lack of Knowledge

Bad code stems from a lack of knowledge, not malice, even though both bad code and malice share unawareness as their root cause. Sometimes, it helps to put on a "lack-of-knowledge hat" to better understand the intentions behind the code you're reading.

### Lack of Knowledge II

An interesting feature of inexperience is that it imposes limits on a software system's ability to scale. Software written with unawareness at its core will eventually become rigid and nightmarish, to the point where team members start avoiding the "dark forest" of its codebase. The natural consequence is that such software reaches an upper bound of complexity. Paradoxically, this means that someone tasked with re-engineering it will often find its complexity manageable in the end.

## Testing

- If you do not write tests you will never learn how to write them, it is better to write bad tests then not to write any.
- Ability to do TDD is not about black and white: “can or can not”, it is about having 1001 things in your toolbox: techniques, patterns, tricks and hacks - when you have enough of them you can test almost everything in a reasonable amount of time.
- “Legacy code is a code without tests” (“Working effectively with Legacy Code” by Michael Feathers).
- On top of being useful for Quality, Testing is an important prerequisite for Simulations which are essential for complexity management: if I can test, read simulate, every aspect of my program, this means that I can still manage its complexity and vice versa - if my app has blind-spots: areas that are hard or impossible to test, I don't have any control over those areas and have to resort to testing of my app in the wild, outsourcing the quality of my app to the real users.
- “If you can't measure it then it can't be called engineering” (taken from “Object-Oriented Software Engineering: A Use Case Driven Approach” by Ivar Jacobson). We of course also read “measure” as “test” which is another way of measurement.
- Ideally, we should be able to test everything. If something is hard to test,
  it usually means our code quality or the corresponding toolset and testing 
  infrastructure are not yet where they need to be. However, with effort, we 
  can improve them and get there. If you're unsure how to test something 
  properly, start with the simplest, "ugliest" approach: stub everything in 
  a basic way, stub the network in a simple manner, assert what you need to 
  assert, and only then iterate on refactoring both the test and the system 
  under test (SUT).

## Distribution

### Provide Basic Test Sequences with Your Product

If you are a provider of software or hardware, consider going beyond the 
standard "interface control document" (ICD) by including basic test 
sequences – a "Hello World"-type program that allows users to quickly get 
started with your product. Such examples help users bring the system online 
and get up to speed without unnecessary guesswork.

The lack of clear "Hello World" or how-to documentation is especially 
prevalent in the embedded software industry, where companies often rely 
solely on ICDs or technical reference manuals. This forces end-user software 
engineers to engage in guesswork and reverse-engineer the documentation to 
figure out how to bring up a device. While the industry is gradually 
improving in this regard, there is still a long way to go. By providing a 
clear and functional "Hello World" example with every product, you empower 
your users and make adoption of your product much smoother.

### Provide Drivers Alongside Your Hardware

If you are a hardware provider, consider supplying software drivers with 
your device rather than just a technical reference manual for end-users to 
decipher and implement. As the developer of the device, you understand its 
functionality better than anyone else. By providing ready-to-use drivers, 
you save your users the time and effort of implementing the device's 
features themselves.

With some effort on your part, you can significantly improve the adoption of 
your product by making it easier to integrate and use. A smooth setup 
process not only enhances user satisfaction but also reduces the barriers to 
bringing your hardware to market.

## Reliability

### Errors are not ok

Never ignore errors. Presence of errors indicates that you don't understand your
system well enough and therefore don't have a full control over it.

An error can be major or minor but it anyway contributes negatively to the
design and operation of your system and also to your understanding of it (see
[Periphery](#periphery)).

Errors typically ignored by developers include:

- Configuration errors
- Compiler warnings
- Build system errors
- Errors produced by the test suites (flaky tests)

### Errors must be understood and described

Google for `Malfunction 54` for a good example.

### Underlying errors shall not be hidden

If a higher-level error wraps some other underlying error, the information
about the underdying error shall not be lost. Instead, it should be fully available
to the higher-level error for error handling, logging, tracing, etc.

### Critical errors vs non-critical errors

Make a clear distinction between critical and non-critical errors on all levels:
source code, software design, error reporting, documentation.

### Assertions are better than no error handling

When there is no error handling, presence of asserts gives at least some basic
guarantee that software does not do what it is not supposed to.

### Assertions are shortcuts for a proper error handling

Every assert becomes a proper error handling eventually.

## Systems

### Good enough is often best

"Good enough for each part is often best for the whole system." ("The Art of
Systems Thinking")

In "Engineering a Safer World", Nancy Leveson discusses how, in air traffic control, individual flight paths may not be optimized for each aircraft to ensure overall traffic harmony. This approach is necessary because optimizing each flight path individually could lead to conflicts and inefficiencies. Instead, air traffic control systems manage traffic by coordinating flight paths to maintain safe separation between aircraft, ensuring the overall safety and efficiency of the airspace.

### Designing Systems for Effective Work

- "Rather than trying to find extraordinary people to do a job, design the job so
that ordinary people can do it well." ("The
Art of Systems Thinking")

> ...No one comes to work to do a bad job, but the structure of the system may
make good work impossible. If management falls into the blame trap, they may
fire the offending individual and hire someone else - who may do no better.
Rather than trying to find extraordinarypeople to do a job, design the job so
that ordinary people can do it well. It is the structure of the system that
creates the results. For better results, change the structure of the system.

## People and Organizations

### Everyone is busy

Everyone is busy, including you. The development of software products often 
takes place in rushed environments, where everyone is focused on achieving 
specific goals without having time to do things properly or fully explore 
all the options for what is being built.

How about QA? A company may have a dedicated QA department, or even Safety & 
Reliability teams in addition. They are most likely also busy, focusing on 
the most critical tasks to the point that they probably don't have enough 
time to interact with development teams, understand the real requirements, 
or provide 100% coverage and a complete assessment of the project scope.

Is it a problem that everyone is busy? Given its ubiquity, it doesn't seem 
so. Some people even seem to thrive on being busy all the time. 
Organizations appear to care little about “busyness” itself. What really 
matters is whether the busy person or department can deliver results 
according to the schedule or whether something left uncovered by the busy 
teams could create serious problems for the business.

One unfortunate observation is that it usually takes significant time before 
the uncovered issues are revealed and addressed from the top down. During 
this incubation period, enough money is often lost, a number of unhappy 
customers accumulate, and other losses may occur, depending on the type of 
project.

Or, busy people themselves get tired... and create new methods and tools. 
Sometimes, a new tool can eliminate much of the effort required to achieve a 
goal, or it simply allows a busy person to focus on "what is most important" 
rather than covering everything.

### Four seasons

It is an amusing analogy: like a year starts with a spring and ends with a
winter, a similar lifecycle can be observed in a growth of organizations.

Spring is a young company, a handful of people. Not much structure, no strict
policies, a startup atmosphere. Not yet a fixed income, but probably
investments or lack of them. More full-stack people with broad expertise.
Spring is like a village. Colleagues are fellow villagers.

A Summer is a Spring that made it, a company that is flourishing. Exponential
growth, more people are hired, extremely steep curve of everything:
the development of the company structure, more departments, more specialization.
The philosophy of the company is no longer about "finding its way" but rather
accelerating on what made a transition from Spring to Summer possible.

Autumn is already a company with legacy. The source of income is known and
stabilized. The responsibilities are defined. Less or no people are busy with
defining a product anymore but more people are busy with the optimization:
improving product, doing sales and increasing revenues.

Winter is a dangerous phase. The company has been making profit and doing its
best by exhausting what was known to work well. At this point, the structure of
the company is the most fixed and therefore the least resilient. The company may
cease to exist because there are younger and more adequate competitors or it can
find a way to renew itself and make it into a new year.

Another interesting observation is that a transition from season to season
almost never goes smoothly – in order to accomodate for change, the company
has to adapt and this very often happens with a good deal of destruction and
restructuring (see Prima Materia heuristic). Dropping what does not work and
keeping or creating what does might be crucial for such a transition. Not all
of the Spring companies make it into Summer. Not all of the companies end up
being Winter. Not all of the companies can survive their deep Winter.

One particular management mistake that can be made is trying to apply the best
practices of a season A to a season B if the season B is too early or already
too late for such an application. Example: imposing a strict top-down style of
management on a company of 5-10 people working in a flat hierarchy and making
them to adhere to the reporting lines might be extremely inadequate as well as
expecting a fully flat hierarchy to work in an Autumn-like business.

Not only we can match seasons and companies, we can also match seasons and
personalities:

- Autumn is too boring for spring people who value creativity and individual
contribution over hierarchies and defined processes.
- For Autumn people, the Spring is too chaotic and unstructured. Working for a
Spring company is inherently unsafe: the younger the company, the less
guarantees it can provide to its employees.
- It may not be optimal for a company to have too many people who represent
an incompatible season. It can be damaging for a person to get stuck working
at a company that does not match their season type. In such cases, a person who
found a matching season can be compared to a fish that found its water.

See also Kent Beck's
[The Product Development Triathlon](https://medium.com/@kentbeck_7670/the-product-development-triathlon-6464e2763c46). His 3 phases:
Explore-Expand-Extract can be loosely mapped to the Spring-Summer-Autumn
seasons.

## Meetings

### Sound Check

It's great when everyone joins a meeting on time, but an often-overlooked practice is doing a quick sound and video check to ensure everything is working smoothly. A good rule of thumb is to join:

- 5 minutes early for routine meetings.
- 15–30+ minutes early for important meetings, to handle any technical issues in advance.

### Meeting Agenda

A well-prepared meeting runs smoothly when attendees know what to expect.

- A strong meeting has a predefined agenda that allows participants to follow a clear execution plan.
- Is the agenda known in advance?
- Can you or your team define it?
- Are there questions or answers that can be prepared beforehand?

### Meeting Notes

Meetings often lack structure, and when no notes are taken, valuable discussions can be lost. A better approach is for someone to take ownership of note-taking in real-time, ideally on a shared screen so everyone can see what is being recorded.

- If your team owns the agenda, align meeting notes with the planned topics.
- Structure notes so key points and next steps are clear.

### Capturing Meeting Results

A meeting without tangible outcomes is just an expensive conversation. At a minimum, meetings should result in:

- Action points: tasks, follow-ups, next meetings.
- Decisions made.
- Recognized trade-offs.

Whenever possible, capturing processes or architectures in a diagram is better than a simple bullet point. Even if no formal notes are recorded, every participant leaves with takeaways and mental models — but written records significantly increase the meeting’s effectiveness.

Anti-pattern: Running meetings without documenting useful outcomes, leading to wasted time and repeated discussions.

### Briefing In

Before the actual meeting, getting alignment among participants is key, whether for internal team discussions or external events like conferences and large review meetings. When a team participates in an external meeting, it is crucial that everyone is on the same page and presents a unified front, avoiding any visible disagreement or misalignment.

Good questions to determine if a pre-meeting briefing is needed:

- How many attendees already know what will be presented?
- Does the content introduce significant innovation that requires prior context? Could too much new information create confusion within the presenting team?

Common pitfalls:

- Discussing internal team matters in the presence of external participants.
- Asking too many unrelated questions that derail the focus of the meeting, particularly when it disrupts team cohesion and diverts attention from the main agenda. This is especially problematic when an individual undermines the shared position of the team by introducing misalignment.

### Sharing Screen & Presenting Material

- Share only the relevant content—close unrelated applications, especially internal company chats, before presenting to an external audience.
- If you need to access other files or perform actions outside the presentation, unshare your screen first, complete the task, then reshare only the necessary content.
- If your team is presenting to an external party, align on the materials beforehand to ensure consistency in messaging.

## Biases

### The Working-So-It's-Right Bias

The issue lies in assuming that a previous solution or setup is correct simply because it works. This leads to a lack of scrutiny, where the existing solution or setup is not questioned, and investigations proceed based on a flawed premise.

### The Fix Bias

When reviewing a pull request titled "Fixes XYZ," there is a natural tendency to trust the new change more than the existing code. This bias arises from the assumption that the previous implementation was flawed simply because it is being replaced. As a result, one might overlook the consequences of the fix or fail to rigorously verify the correctness of the new change.

To mitigate this bias, it's important to evaluate both the old and new implementations with equal scrutiny. Consider questions such as:

- Is the problem being solved accurately identified?
- Does the new change address the issue without introducing new problems?
- Are the trade-offs of this fix justified compared to the original implementation?

By being aware of this bias, reviewers can ensure a more balanced and thorough review process.

### Resolving Merge Conflict Bias

Software engineers frequently resolve merge conflicts, and while this task is often trivial, it presents opportunities for introducing subtle bugs. One contributing factor is the cognitive bias that favors accepting newly introduced changes over preserving existing behavior.

The conflict markers (`<<< >>>`) used by Git can obscure important details of the original code, making it easy to unintentionally discard necessary logic.

A practical approach to mitigating this risk is to slow down and carefully evaluate both conflicting versions. Consider not just the new change, but also what might be lost if an existing line or code chunk is removed. Reviewing the code in context and testing after resolving conflicts can help prevent unintended regressions.

## Documentation

- Good documentation is dry and boring. This can create an illusion that writing
good documentation is easy when in fact it is not.

### Less prose, more structure

Technical documentation is supposed to focus engineer's attention on achieving
a given goal such as to build a specific system. It is easier to focus one's
attention on things that have structure embedded in them compared to things
that are hidden in several paragraphs of prose. Prose has no structure and
that is why a reader has to do an extra exercise of creating an order out of
what he is reading. If the documentation already has an order in it, the reader
can spend less time for a mental reconstruction of the content and focus on
the technical facts more easily.

Some of the important tools that communicate order in technical documentation:

- Document structure and table of contents
- Diagrams
- Tables.

### Too Much Structure Overload

Excessively deep nesting in documents or folder structures can hinder the 
understanding of the overall project or system structure, especially if the 
principles used for organizing the sections lack consistency. Ideally, a 
good structure should be intuitive, or at the very least, the organizational 
principle should be easy to understand and mentally map, facilitating easier 
navigation of the content.

### Encyclopedic Document

An encyclopedic document is created over time as a collection of inputs from
various ad hoc events, eventually becoming a generic repository of 
everything. These documents often have complex, nested structures and lack a 
single consistent narrative. Reading them feels more like going through a 
dictionary from A to Z rather than following a coherent story. This can make 
it difficult for readers to stay engaged, which might explain why many 
people shy away from reading standards altogether.

Standards or guidelines are often structured in this encyclopedic way, as they 
aim to encompass all aspects of product development or organizational 
processes. Similarly, requirements specifications can easily take on an 
encyclopedic form, making them hard to navigate and comprehend.

When creating such documents, it’s important to establish a guiding 
principle that helps readers mentally map and navigate the content. Ideally, 
the document should include a unifying narrative or story that makes it 
easier to follow, even if the underlying information is complex or diverse. 
A clear structure and logical flow can transform an overwhelming collection 
of information into a useful and accessible resource.

## Standards

### Idealized standards vs. practical implementation

Standards provide an idealized or encyclopedic view of how systems should 
function and how products should be developed. Frequently, a standard 
represents the combined inputs of multiple companies, making it more 
extensive than what any single company might realistically implement. For 
most companies, implementing a standard is a "best effort" exercise.

Some standards are practical only for larger companies and can be 
counterproductive or harmful for smaller organizations attempting to 
implement them. Recognizing this, some standards explicitly account for a 
company's maturity level and offer recommendations on which parts to 
implement at different stages of development.

### The challenge of standards implementation

Implementing standards and managing their results within an organization can 
be difficult and complex. However, without any standards, everything becomes 
10 to 100 times harder and more chaotic.

### Standards and best practices

Standards seek out best practices, collect them, and generalize them.

### Standards favor good practice

Standards favor good practices. If a company has adopted a practice that is 
not yet conventional but makes sense and adds value, it is unlikely that 
this practice would be rejected or deemed inappropriate by any standard.

### Wrong is worse than early or incomplete

Sometimes it is worse to be wrong than to be early or lack information.
The context: passing the project review milestones required by standards.

## Requirements

### One-stop shopping

> "One-stop shopping" is a useful requirements writing priciple. Simply, people
reading the requirements should be able to get all the information they need
from one document or from one section of a document. They should not have
to jump between different sections to understand the requirement.
(Patterns for Effective Use Cases by Steve Adolph et al., Chapter 7.1)

## Safety

### Safety does not exist without blood, loss or failure

Safety is not there from the very beginning. A gloomy poet could say
that safety blooms on blood. Safety does also not exist on its own: you first
need to build something that kills people or causes a loss, then some people
will bother to learn from this and take actions. Only then safety gets
recognized and truly appreciated.

Consequence: safety is especially sound for those folks who have some
experience of dealing with blood, loss or failure.

### Safety is boring

When implemented well enough, safety becomes boring. Everything is working, no
one complains. At that moment, it is easier than ever to forget about why the
safety is there in the first place. Example: how often do we bother to look at
the safety manuals? Does it mean that the safety is there?

### Safety is very hard to achieve but is very easy to lose

Safety is the extremely fragile and sensitive property of the systems. It so
much effort that is put into achieving it and still it is so easy to let the
whole system get down. Some of the very popular reasons for the failure are:

- degradation of existing components
- changes to the system that do not take the current system's behavior into
account
- new unexpected factors coming outside the system boundary

Consequence: safety requires continuous and intelligent effort.

### Success breeds failure

Handbook of Walkthroughs, Inspections, and Technical Reviews, p.412:

> ... however, we have to anticipate that we will in fact succeed once in a 
> while - and we must also anticipate what that success will bring. For 
> instance, one error-riddled system was seldom used by its several hundred 
> potential users, so management decided to mount an effort to have the 
> system repaired in a systematic fashion. The resulting system was so 
> dependable and useful that usage suddenly increased by a factor of a 
> thousand over previous usage. This increase in transaction volume made the 
> file design of the system completely inadequate to the daily load - which 
> soon meant that nobody could get results fast enough to be useful. The 
> entire problem - and so many others like it - could have been avoided if 
> the review group had only considered that unavoidable law of nature:
> **Success breeds failure**. So, ..., be prepared for the inevitable 
> reaction. If you start making systems better, your users will want more of 
> the same - the best side effect of all.

### Safety as a Defensive Discipline

Safety is often seen as a defensive discipline, in contrast to fields focused on
creation, innovation, and action, which drive progress. While these fields 
push forward with new ideas and developments, safety functions as a 
secondary, backing force. Its role is to prevent harm, minimize risks, and 
ensure that these actions happen within a secure framework. Safety doesn't 
seek to lead the charge but to protect and enable other processes to unfold 
without catastrophic failure.

However, the drive to "lead the charge" often means safety is ignored or 
sidelined until it's too late. In this way, safety acts like a belt that 
holds uncontrolled progress together, preventing it from falling apart when 
the inevitable risks are not properly addressed.

### Safety for Engineering is Like Medicine for People

Medicine isn't the most exciting thing, and no one wants to spend all their 
time thinking about it. But it's clear that humanity can't thrive without it,
even with all the amazing achievements of civilization.

In the same way, organizations focus on building things that work and often 
don't think much about safety or quality as long as things are fine and 
customers are happy. But over time, they may realize that the "health" of 
their products, teams, and development processes also matters.

How safety and quality are handled depends a lot on experience and knowledge.
Not long ago, amputation was seen as the best way to treat many illnesses. 
This shows how much we've learned and how practices improve over time. 
Engineering also needs to grow in this way, moving beyond quick fixes to 
create stronger, longer-lasting solutions.

### User Interfaces and Critical Systems

Too much simplicity can be a problem. Overly simplistic interfaces may 
prevent operators from engaging their brains fully, which could negatively 
impact their performance in critical situations. If an interface is too 
simple, operators can fall into automatism, executing the wrong action due 
to a lack of alertness. There are serious concerns that software and 
interface designers should prioritize preventing user mistakes, rather than 
focusing solely on aesthetics.

## Books

- [The Art of Systems Thinking](https://www.google.de/search?q=the+art+of+systems+thinking+book&oq=the+art+of+systems+thinking+book)

## Similar resources

- [Kent Beck - Mastering Programming](https://www.facebook.com/notes/kent-beck/mastering-programming/1184427814923414/)
- [Heuristics of Software Testability](http://www.satisfice.com/tools/testable.pdf)
- [The Law of Leaky Abstractions](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)
- [Lessons Learned in Software Development](https://henrikwarne.com/2015/04/16/lessons-learned-in-software-development/)
