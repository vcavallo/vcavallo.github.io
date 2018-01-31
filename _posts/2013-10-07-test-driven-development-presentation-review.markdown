---
layout: post
title: "Overview Test-Driven Development"
date: 2013-10-07 21:52
comments: true
categories: presentations tdd tes-driven development rspec speakerdeck
excerpted: true
---

A little overview of TDD, written at a time when I had just learned about it myself.

<!--more-->

Earlier tonight I was flipping through [Jason Arhart](https://github.com/jarhart)'s [Speakerdeck presentation](https://speakerdeck.com/lvrug/introduction-to-tdd-jason-arhart) on the basics of Test-Driven Development and giving a little thought to the topic in general.  
For starters:

### A little overview of TDD

TDD is a system in which you create a suite of tests to ensure your code stays in line during development. It takes advantage of a few truisms that surround programming:

- Repetition is key to testing
- Computers are good at repetition
- ~~Humans~~ Programmers like automating repetitive tasks

> "Why use TDD instead of whatever it is I normally do?"  
> - You, sounding a bit silly.

Well, see what you said there? The second part of the sentence? You most likely have a general plan for your code, write a little, play with it and see if it breaks, write a little more, etc. Before you know it you've got a whole bunch of code, testing it becomes cumbersome and your test coverage starts to get a little spotty. Worst of all, you don't know when you're missing something. - That is, until something breaks a little later. 

> "Ok, I guess that doesn't sound so smart. What's this thing you're talking about?"  
> - You again, wising up.

This thing is **[test-first development](http://en.wikipedia.org/wiki/Test-driven_development)**. Before you write a line of production code, you're going to write at least one (failing, for now) test that describes what your program *should* do when it's working properly. By keeping the end goal in your sights you minimize the risk of diluting your focus throughout the coding process.  

- You start with a failing test and then write only enough code to make it pass  
- Then you write some more tests (a bunch, if you like) and write only enough code to make each of those tests pass, in order.  
    - (check out the `--fail-fast` flag, when the time is right).  


All of this careful attention to the intended end result has an added bonus, as if having working code isn't pleasant enough: Refactoring is safer and more fun. The adage goes: 

## <span style="color:red">Red</span> | <span style="color:green">Green</span> | <span style="color:blue">Refactor</span>

And then **[repeat]**. Once you've got passing tests, refactor, look out for red (make it pass again) and continue. Never refactor unless all your tests pass.  
It nicely echoes [Kent Beck](http://en.wikipedia.org/wiki/Kent_Beck)'s "Make it Work, Make it Right, Make it Fast". 

> "That sounds great! Aren't there any downsides, though?"  
> - You, bringing up a good point...

**"Sure"**. is the answer. **"False Positives"** is one elaboration of that answer. There is no clear way to test *the tests*, aside from being really careful and diligent when writing them - but even then there are bound to be mistakes sometimes. That's the whole reason you write tests to begin with: to account for your mistakes or normal human inability to complete every complex task with 100% accuracy on the first try.  
Another pitfall is the tendency to veer towards [The Happy Path](http://en.wikipedia.org/wiki/Happy_path) whenever possible. Your tests are only as good as your natural or tailored skepticism. Doubt yourself often and rigidly.

## A final thought that intrigues me

...in the context of TDD. Looking at a full suite of tests with its   
`such-and-such method should do this-thing`  
evokes a curious idea... *Yes, that method should do that thing. Why should I have to tell it how?* It seems like having a computer figure out how some not-yet-written code should behave based on some simple human-readable instruction is the next logical step in the process. As a programmer, you switch gears from "Test-Designer Overlord" to "Code Implementer Monkey" during the TDD process. Doesn't the former sound more human and the latter more machinated? The same way an automatic transmission knows to shift when we want the car to drive at a certain speed, how long do we have to wait until an interpreter knows how to write a method, given some discrete instructions? Uh oh, sounds like some(many thousand)one would be out of a job!

## Further TDD Reading?
Check [This](http://betterspecs.org/) out. 
