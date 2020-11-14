# Software Design Heuristics

These are the heuristics that I find useful in my software engineering practice.
I call "heuristics" everything that helps me to write better code given that
I have them in mind.

Some heuristics are of my own, sometimes I also learn from good books.
Heuristics here that are cited always have reference to their source.

All of these heuristics work only if taken all together. Taken away from the rest,
some of them can even contradict each other: if you take only a few of them and
exaggerate them, they will lose their value or even break things on your behalf.
Some heuristics may overlap with each other. So do not be very serious about
them.

Currently this is just a draft, very far from complete, with some random notes
arbitrarily organized, do not expect it to be solid.

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
  - [Other](#other)
- [Complexity and Cognitive Load](#complexity-and-cognitive-load)
  - [Black Box with a Green Play Button](#black-box-with-a-green-play-button)
  - [Humans are not designed for Big Numbers](#humans-are-not-designed-for-big-numbers)
  - [There is no such thing as Many](#there-is-no-such-thing-as-many)
  - [0-1-2-Many I](#0-1-2-many-i)
  - [0-1-2-Many II](#0-1-2-many-ii)
  - [Periphery](#periphery)
  - [Solving Right Problems](#solving-right-problems)
- [Design](#design)
  - [Poor Abstraction](#poor-abstraction)
  - [Hard Feature](#hard-feature)
  - [True Name](#true-name)
  - [One Pattern per Class](#one-pattern-per-class)
  - [Archetype](#archetype)
  - [Trade-off of Encapsulation](#trade-off-of-encapsulation)
  - [Unnecessary Flexibility](#unnecessary-flexibility)
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
- [Reliability](#reliability)
  - [Errors are not ok](#errors-are-not-ok)
  - [Errors must be understood and described](#errors-must-be-understood-and-described)
  - [Underlying errors shall not be hidden](#underlying-errors-shall-not-be-hidden)
  - [Critical errors vs non-critical errors](#critical-errors-vs-non-critical-errors)
  - [Assertions are better than no error handling](#assertions-are-better-than-no-error-handling)
  - [Assertions are shortcuts for a proper error handling](#assertions-are-shortcuts-for-a-proper-error-handling)
- [Maintenance Programming](#maintenance-programming)
  - [Stable Components](#stable-components)
  - [Boring Code](#boring-code)
  - [Boring Code 2](#boring-code-2)
  - [Ignorance](#ignorance)
  - [Ignorance II](#ignorance-ii)
  - [Other](#other-1)
- [Systems](#systems)
- [People and Organizations](#people-and-organizations)
  - [Everyone is busy](#everyone-is-busy)
  - [Four seasons](#four-seasons)
- [Safety](#safety)
  - [Safety does not exist without blood, loss or failure](#safety-does-not-exist-without-blood-loss-or-failure)
  - [Safety is boring](#safety-is-boring)
  - [Safety is very hard to achieve but is very easy to lose](#safety-is-very-hard-to-achieve-but-is-very-easy-to-lose)
  - [Safety for engineering is the same as medicine for people](#safety-for-engineering-is-the-same-as-medicine-for-people)
- [Testing](#testing)
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
having to think deeply about where it is. It’s something like clarity, but clarity is
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

Lots of what we programmers learn with years comes from a pain not from a good will.

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

### Other

- Don't give your classes plural names. One example is a test class which is
based on a xUnit framework. Don't call it plural, call it singular:
your class gives you an instance that exercises **many** tests but the class and
instance is one. `UserTest`, not `UserTests`! See also "There is no such thing
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

## Design

### Poor Abstraction

> Duplication is better than poor abstraction (Sandi Metz, Rails Club 2014, Moscow).

> "...ill-fitting structure is worse than none..." (Eric Evans - Domain-Driven Design, p.446)

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
and coherent. If you know the archetype of something you understand the essense
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
- Separate construction from operation (one example: Factory vs Command)
- Separate content from presentation (applies to UI-heavy code, great example: HTML/CSS)
- Separate easy from complex: isolate easy, isolate complex, repeat many times (todo: separation vs isolation)
- Separate stateless from stateful
- Separate data from behavior and behavior from data unless you do have a good
OOP class/object with good data/behavior balance.
- Separate general-purpose from application-specific
- Separate application-level code from system-level code
- Separate methods that read from methods that write
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

Group together things that change at the same time. If possible create container
data structures so that a change involves a change of **one**. If possible,
group all of the changes that happen at the same time together.

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

### Ignorance

Bad code comes from ignorance, not from evil will, inspite of the fact that both
bad code and evil will share ignorance as their root. Sometimes it helps a lot
to wear imaginary ignorance hat to understand an intention behind a code you're
reading.

### Ignorance II

One interesting feature of Ignorance is that it imposes a limit on ability of a
software to scale. Written with ignorance in mind software sooner or later
becomes a stone and nightmare so that eventually programmers on a team start to
avoid going to "the dark forest". Natural consequence is that such software has
an upper bound of complexity so someone who has to re-engineer such code will
find that that complexity is ultimately manageable.

### Other

- Always leave code in a better state than it had been before you got it, save a
time for future you or someone else to make it even better (dedicated to folks
who enjoy fixing things "in just a few minutes").

## Systems

- "Good enough for each part is often best for the whole system." ("The Art of
Systems Thinking")

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

Everyone is busy, including you. Development of software
products often happens in rushed environments where everyone is busy
achieving given goals without having time to do things properly or at least
fully realize all options of what is being built.

How about QA? A company might have a QA department or even Safety & Reliability
people in addition. They are most likely also busy: they focus on the most
important things, so much that they probably don't have enough time to interact
with development teams, understand what is really required or provide 100%
coverage and complete assessment of project scope.

Is this a problem that everyone is busy? Given the ubiquity, it doesn't seem so.
Some people even seem to like being busy all the time. It looks like
organizations don't care much about "busyness" at all, what really matters is
how that busy person/department is able to produce on given schedules or if
something not covered by the busy people can create serious problems
to the business. One sad observation about this is that it usually takes
significant time until the uncovered is revealed and fixed top-down. During this
incubation period, enough money should be lost, number of unhappy customers
accumulate, and all other kinds losses, depending on the type of a project.

Or busy people themselves get tired... and create new methods and tools.
Sometimes a new tool can eliminate a lot of effort required to achieve a given
goal or it simply allows a busy person to focus on "what is most important"
instead of covering everything.

### Four seasons

It is an amusing analogy: like a year starts with a spring and ends with a
winter, a similar lifecycle can be observed in a growth of organizations.

Spring is a young company, a handful of people. Not much structure, no strict
policies, a startup atmosphere. Not yet a fixed income, but probably
investments or lack of them. More full-stack people with broad expertise.

A Summer is a Spring that made it, a company that is flourishing. Exponential
growth, more people are hired, extremely steep curve of everything:
the development of the company structure, more departments, more specialization.
The philosophy of the company is no longer about "finding its way" but rather
accelerating on what made a transition from Spring to Summer possible.

Autumn is already a company with legacy. The source of income is known and
stabilized. The responsibilities are defined. Less or none people are busy with
defining a product anymore but more people are busy with the optimization:
improving product, doing sales and increasing revenues.

Winter is a dangerous phase. The company has been doing its best by exhausting
what was known to work well and making profit. At this point, the structure of the
company is the most fixed and therefore the least resilient. The company may
cease to exist because there are younger and more adequate competitors or it can
find a way to renew itself and make it into a new year.

Not all of the Spring companies make it into Summer. Not all of the companies
end up being Winter. Not all of the companies can survive their deep Winter.

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
- For Autumn people, the Spring is too chaotic and unstructured. Working a
Spring company is inherently unsafe: the younger the company, the less
guarantees it can provide to its employees.
- This may not be optimal for a company to have too many people who represent
an incompatible season. It can be damaging for a person to get stuck working
at a company that does not match their season type. In such cases, a person who
found a matching season can be compared to a fish that found its water.

See also Kent Beck's
[The Product Development Triathlon](https://medium.com/@kentbeck_7670/the-product-development-triathlon-6464e2763c46). His 3 phases:
Explore-Expand-Extract can be loosely mapped to the Spring-Summer-Autumn
seasons.

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
- new unexpected factors coming outside of the system boundary

Consequence: safety requires continuous and intelligent effort.

### Safety for engineering is the same as medicine for people

Medicine is not the most important thing in this world and no one wants to
spend all time on it. But it is also true that we humans will not
go far away without medicine even with all other achievements of our
civilization at hand.

Like it is with human beings, organizations want to build things that
work - they are less concerned with things such as Safety or Quality as long as
everything is fine at first and the customers are satisfied. Then it might
happen to them that the "health" of the product, team and development process
also matter. The implementations may depend on the prior knowledge and
experience - not so long ago the best treatment for many of the human body
diseases was the amputation.

## Testing

- If you do not write tests you will never learn how to write them, it is better to write bad tests then not to write any.
- Ability to do TDD is not about black and white: “can or can not”, it is about having 1001 things in your toolbox: techniques, patterns, tricks and hacks - when you have enough of them you can test almost everything in a reasonable amount of time.
- “Legacy code is a code without tests” (“Working effectively with Legacy Code” by Michael Feathers).
- On top of being useful for Quality, Testing is an important prerequisite for Simulations which are essential for complexity management: if I can test, read simulate, every aspect of my program, this means that I can still manage its complexity and vice versa - if my app has blind-spots: areas that are hard or impossible to test, I don't have any control over those areas and have to resort to testing of my app in the wild, outsourcing the quality of my app to the real users.
- “If you can’t measure it then it can’t be called engineering” (taken from “Object-Oriented Software Engineering: A Use Case Driven Approach” by Ivar Jacobson). We of course also read “measure” as “test” which is another way of measurement.
- Ideally we should be able to test everything: if something is hard to test, then we are just not there with quality of our code or corresponding tool set and infrastructure for testing but we will manage to find or improve them and get there.
If you don’t know or not sure how to test something properly, try the ugliest version first: stub everything in an ugly way, stub network in an ugly way, assert what you want to assert and only then iterate on refactoring of both test and SUT (system-under-test).

## Books

- [The Art of Systems Thinking](https://www.google.de/search?q=the+art+of+systems+thinking+book&oq=the+art+of+systems+thinking+book)

## Similar resources

- [Kent Beck - Mastering Programming](https://www.facebook.com/notes/kent-beck/mastering-programming/1184427814923414/)
- [Heuristics of Software Testability](http://www.satisfice.com/tools/testable.pdf)
- [The Law of Leaky Abstractions](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)
- [Lessons Learned in Software Development](https://henrikwarne.com/2015/04/16/lessons-learned-in-software-development/)
