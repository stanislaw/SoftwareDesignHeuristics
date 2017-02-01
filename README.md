# Heuristics 1001

These are the heuristics that I and some of my colleagues find useful in our software engineering practice. We call “heuristics” everything that helps us to write better code given we keep them in mind.

Some heuristics are of our own, sometimes we also learn from good books: heuristics here that are cited always have reference to original.

All of these heuristics work only if taken altogether. Taken away from the rest, some of them can even contradict each other: if you take only few of them and exaggerate them, they will lose their value or even break things on your behalf. Some heuristics may overlap with each other. So do not be very serious about them :)

Currently this is just a draft, very far from complete, with some random notes arbitrarily organized, do not expect it to be solid. If still this folklore genre works for you, feel free to share heuristics you might have in mind.

## General

- **Start Simple.** Start with something simple, then extend it further. Most often a complex problem is a composition of simpler problems. If you are facing a problem and you are afraid of the complexity it exerts, try to make a smallest possible step towards the solution and see what you can do from there. Simple can also mean quick and dirty but that's ok as that's only a start. Once you have something simple working you have a ground to move on further. Most likely this means you have an **archetype** of a future thing: real and complex system. 

See also Kent Beck's [Test-Driven Development book](https://en.wikipedia.org/wiki/Test-Driven_Development_by_Example) where this approach of doing simple things is explained at great depth.

- **Archetype.** Archetype is an umbrella concept for other concepts like: `prototype`, `proof of concept`, `minimal viable product`. Archetype means something simple and coherent. If you know the archetype of something you understand the essense of it. A complex system can be traced back to a one or a number of underlying archetypes.

Interesting side note: as far as I see it, the tendency is that engineers as they grow their software bigger, do not care much 
about the underlying archetypes. Imagine how easy it would be to learn about the software if it would contain itself in its earliest forms of being (source code, documentation, drafts etc). Great example: Rust programming language had to be started from [somewhere](https://github.com/graydon/rust-prehistory).

- **Habitability**. Habitable software is better than perfect software, both for its users and its developers (Richard Gabriel - Patterns of Software).

- Poor Abstraction Heuristics.

> Duplication is better than poor abstraction (Sandi Metz, Rails Club 2014, Moscow).

> "...ill-fitting structure is worse than none..." (Eric Evans - Domain-Driven Design, p.446)

- If feature is hard to implement it might indicate that it is something wrong with feature (or product).

- If you know [True Name](https://en.wikipedia.org/wiki/True_name) of something you have power over it. Good class - this is what True Name is in OOP. See also [Mass and Gravity](http://www.carlopescio.com/2008/12/notes-on-software-design-chapter-2-mass.html).
- Prima Materia Heuristics. Sometimes to make further progress you need to un-implement (break!) particular pattern/architecture/solution and put it back into [Prima Materia](Prima materia - Wikipedia, the free encyclopedia) state and only then thansform it into a something new. Metaphors similar to Prima Materia are "primordial soup" and "indifferentiated soup of ideas" (Eric Evans - DDD).

- Always leave code in a better state than it had been before you got it, save a time for future you or someone else to make it even better (dedicated to folks who enjoy fixing things "in just a few minutes").

- Ignorance Heuristics. Bad code comes from ignorance, not from evil will, inspite of the fact that both bad code and evil will share ignorance as their root. Sometimes it helps a lot to wear imaginary ignorance hat to understand an intention behind a code you're reading.

- Ignorance II Heuristics. One interesting feature of Ignorance is that it
imposes a limit on ability of a software to scale. Written with ignorance
in mind software sooner or later becomes a stone and nightmare so that
eventually programmers on a team start to avoid going to "the dark forest".
Natural consequence is that such software has an upper bound of complexity so
someone who has to re-engineer such code will find that that complexity is
ultimately manageable.

- Crash Early Heuristics. If you know how to not program defensively in a particular situation go ahead! Otherwise make your code to Crash Early to catch bugs as early as possible: use sensible assertions and stress edge-cases with tests. See [Some notes C in 2016: Code offensively](http://blog.erratasec.com/2016/01/some-notes-c-in-2016.html#.VtGEKBg7T5c) and [Spotify engineering culture (part 2): "We aim to mistakes faster than anyone else"](https://labs.spotify.com/2014/09/20/spotify-engineering-culture-part-2/).

- Fast Feedback Heuristics. Getting feedback fast is essential for an engineer.
The two great ways of getting feedback fast are test-driven development
and debugging techniques. When you come to a new project, first of all learn
how to run existing and write new tests and also learn how can you debug
things the fastest way (can be a real debugger, or just "console.log()").

- Unnecessary Flexibility (from
[Writing Solid Code](http://writingsolidcode.com/))

> Flexibility breeds bugs. Another strategy you can use to prevent bugs is to
strip unnecessary flexibility from your designs... The trouble with flexible
designs is that the more flexible they are, the harder it is to detect bugs.

> ...Flexible features are troublesome because they can lead to unexpected
"legal" situations that you didn't think to test for even realize were legal...

> ...When you implement features in your own projects, make them easy to use;
don't make them unnecessary flexible. There is a difference.
Don't allow unnecessary flexibility.

- **Stable Components Heuristics.** Stable Components is a resort of a 
Maintenance Programmer. One way for a developer to survive in a large legacy 
project is to create stable components or extract them out of existing mess 
of code. Stable component most likely means a testable component: it can be a 
parsing module or API layer or string manipulation helpers. Having such islands
of stability helps a lot to overcome the difficulties of a maintenance 
programming. See also Periphery and Prima Materia Heuristics.

- Two Almost Identical Entities. Over the years I have seen at least three big
units of a hardly manageable legacy code where each of them was built on two
almost identical entities from which one was a subclass of the other.
It seems that historically in all three cases it started with one entity that
accumulated its features along the way, then came the other which was so
similar to the first that programmer avoided extraction of similar modules both
entities had and went with subclassing to get the result quickly.
To these days I still didn't see or create an elegant solution to this problem.

### Complexity

- Black Box with Green Play Button Heuristics. Ideal interface for a system of arbitrary complexity is a black box with a green play button on it - you take the box, press green button and it just works. The second ideal interface is when you also have red button to stop a system.
- Periphery Heuristics. If your reasoning is complicated by cognitive overload that you have after a problem you are trying to solve and there is no obvious way to make a first step towards solution, take a step back and start working with Periphery. Good example is legacy code: poor periphery like bad variable names, wrong responsibilities in classes, even those who are distant to your problem, bad folder structure, etc might look completely irrelevant to the core of your problem but still it contributes to the cognitive overload - try to clean up periphery and you will see that the core of your problem is now more clear and approachable than it was before. Another word for Periphery is Background, see also [Deconcentation of Attention](http://deconcentration-of-attention.com/).

### Control

- One of the key concerns is Control: where control should or should not be, what should have control (be active) and what should not have (passive).
- The lower-level modules should not have control over higher-level modules. It is not only about not having higher-level module imported in lower-level modules and making everything to work through protocols/interfaces but more about what is the flow of control: "what controls what".

### Separation / partitioning

- Separate stable from unstable
- Separate synchronous from asynchronous
- Separate symmetrical from asymmetrical
- Separate construction from operation (one example: Factory vs Command).
- Separate data from behavior and behavior from data unless you do have good OOP class/object with good data/behavior balance.
- Separate application-level code from system-level code
- Separate methods that read and methods that write

## Testing

- If you do not write tests you will never learn how to write them, it is better to write bad tests then not to write any.
- Ability to do TDD is not about black and white: “can or can not”, it is about having 1001 things in your toolbox: techniques, patterns, tricks and hacks - when you have enough of them you can test almost everything in a reasonable amount of time.
- “Legacy code is a code without tests” (“Working effectively with Legacy Code” by Michael Feathers).
- On top of being useful for Quality, Testing is an important prerequisite for Simulations which are essential for complexity management: if I can test, read simulate, every aspect of my program, this means that I can still manage its complexity and vice versa - if my app has blind-spots: areas that are hard or impossible to test, I don't have any control over those areas and have to resort to testing of my app in the wild, outsourcing the quality of my app to the real users.
- “If you can’t measure it then it can’t be called engineering” (taken from “Object-Oriented Software Engineering: A Use Case Driven Approach” by Ivar Jacobson). We of course also read “measure” as “test” which is another way of measurement.
- Ideally we should be able to test everything: if something is hard to test, then we are just not there with quality of our code or corresponding tool set and infrastructure for testing but we will manage to find or improve them and get there.
If you don’t know or not sure how to test something properly, try the ugliest version first: stub everything in an ugly way, stub network in an ugly way, assert what you want to assert and only then iterate on refactoring of both test and SUT (system-under-test).

## Similar resources

- [Kent Beck - Mastering Programming](https://www.facebook.com/notes/kent-beck/mastering-programming/1184427814923414/)
- [Heuristics of Software Testability](http://www.satisfice.com/tools/testable.pdf)
- [The Law of Leaky Abstractions](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)
- [Lessons Learned in Software Development](https://henrikwarne.com/2015/04/16/lessons-learned-in-software-development/)


