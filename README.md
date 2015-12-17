# 1001 Heuristics

These are the heuristics that I and some of my colleagues find useful in our software engineering practice. We call “heuristics” everything that helps us to write better code given we keep them in mind.

Some heuristics are of our own, sometimes we also learn from good books: heuristics here that are cited always have reference to original.

All of those heuristics work for us only if taken altogether. Taken away from the rest, some of them can even contradict each other: if you take only few of them and exaggerate them, they will lose their value or even break things on your behalf. So do not be very serious about them :) 

Currently this is just a draft, very far from complete, with some random notes arbitrarily organized, do not expect it to be solid. If still this folklore genre works for you, feel free to share heuristics you might have in mind.

## General

- Duplication is better than poor abstraction (Sandi Metz).
- If feature is hard to implement it might indicate that it is something wrong with feature (or product).
- Sometimes to make further progress you need to un-implement (break!) particular pattern/architecture/solution and put it back into [Prima Materia](Prima materia - Wikipedia, the free encyclopedia) state and only then thansform it into a something new.

### Control

- One of the key concerns is Control: where control should or should not be, what should have control (be active) and what should not have (passive).
- The lower-level modules should not have control over higher-level modules. It is not only about not having higher-level module imported in lower-level modules and making everything to work through protocols/interfaces but more about what is the flow of control: "what controls what".

### Separation / partitioning

- Separate stable from unstable
- Separate synchronous from asynchronous
- Separate data from behavior and behavior from data unless you do have good OOP class/object with good data/behavior balance.
- Separate application-level code from system-level code
- Separate methods that read and methods that write

## Testing

- If you do not write tests you will never learn how to write them, it is better to write bad tests then not to write any.
- Ability to do TDD is not about black and white: “can or can not”, it is about having 1001 things in your toolbox: techniques, patterns, tricks and hacks - when you have enough of them you can test almost everything.
- “Legacy code is a code without tests” (“Working effectively with Legacy Code” by Michael Feathers).
- “If you can’t measure it then it can’t be called engineering” (taken from “Object-Oriented Software Engineering: A Use Case Driven Approach” by Ivar Jacobson). We of course also read “measure” as “test” which is another way of measurement.
- Ideally we should be able to test everything: if something is hard to test, then we are just not there with quality of our code or corresponding tool set and infrastructure for testing but we will manage to find or improve them and get there.
If you don’t know or not sure how to test something properly, try the ugliest version first: stub everything in an ugly way, stub network in an ugly way, assert what you want to assert and only then iterate on refactoring of both test and SUT (system-under-test).
