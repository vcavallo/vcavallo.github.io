---
layout: post
title: "Understanding Recursion"
date: 2013-10-15 23:09
comments: true
categories: ruby recursion learning teaching cognition
excerpted: true
published: true
keywords: recursion, learning
description: Understanding recursion
---

![Google search result for 'Recursion'](http://vcavallo.github.io/images/google-recursion-smaller.png "google result for recursion")  

Learn yourself a bit about recursion!

<!--more-->

# Understanding Recursion

*Recursion*. What's that? I dunno, should probably Google it….  
<br/>
![Google search result for 'Recursion'](http://vcavallo.github.io/images/google-recursion-smaller.png "google result for recursion")  
<br/>
Very funny, Google. (if you don't understand that joke, you'll understand it when you understand recursion jokes.) A [friendlier web service](http://en.wikipedia.org/wiki/Recursion) starts off this way: "Recursion is the process of repeating items in a self-similar way." The simplest example I can think of might be a spiral - it sort of goes around and in a little, and then goes around and in a little and goes around and in a little, etc.  
<br/>
![A spiral](http://vcavallo.github.io/images/spiral.jpg "a spiral")  
<br/>
Here's another real-world example that is a little more procedural and will get our brains warmed-up to get fully into some real code:  
<br/>

## Real-World Recursion

You're in front of a mailbox with these instructions:   
>*if you are not holding an iPhone in your hand, open the next thing you can.  
repeat.*

Since you have a thing (mailbox) that isn't an iPhone, you open it and find a shipping box. It's a thing that isn't an iPhone so you open it and find an iPhone box. It's not an iPhone and it's a thing: you open it and have both an iPhone and a headphones box. You have an iPhone so you stop. Simple enough?

What if i left out the "if you're not holding an iPhone" part? Your instructions would be:  
>*open the next thing you can.  
repeat.*

You'd have gotten to the iPhone and headphones box part and then opened the next thing you could and you'd have a pair of headphones. Since you're a good instruction follower, you'd maybe tear the headphones open and have some sort of little speaker in your hand. You'd rip that open and have some other electronics wizardry and keep going - before you know it you'd be [ripping apart](http://en.wikipedia.org/wiki/Big_Rip) the fabric of space-time\* - and that's what trying to imagine recursion can feel like if you're approaching it the wrong way: Like the fabric of your brain is being shredded by a guy on a wild hunt for an iPhone. Well, not *specifically* like that, maybe.  
</br>

## Getting closer to the code...

If we were to write the above instructions in psuedocode it might look like this:

```
open_thing(thing)
  if not iPhone, open_thing(next_thing)
end
```

Let's notice and remember a few important things about the above code.  

1. The open_thing method is called inside itself
2. When it is called within itself, the argument it takes is *similar* but not *identical* to the argument it takes outside.
3. There's an **if** somewhere

You could say it is **repeated in a self-similar manner.** It doesn't open the same thing again and again - it opens a *next_thing*. So It's recursive! But in a special way because there's also that **if**. The **if** defines our *Base Case*. The thing that tells us to stop recursing. To avoid tearing open the headphones.  
<br/>

### Pause
-----

I forgot to tell you why I'm writing this. Recursion can be a bewildering topic for some. Before this post my understanding of it danced around the periphery of the concept. Yea, I knew what it meant and how it generally worked and about fractals and all that, but I couldn't *intuit* the workings of it - and more importantly, relative to my current endeavor: I didn't get how the heck a computer makes sense of it. I don't want to take such an interesting, complex and pragmatically useful topic on faith. I want to *get* it. If you feel the same way then please read on. I promise your understanding will be different by the end.   
<br/>

-----

### Back to Learning!

As I see it, the typical confusion when thinking about recursion (in terms of programming) comes from two sources: 

- Poor understanding of how the base case works
- Neglecting to visualize how the computer will interpret your code

The idea of repeated iteration is not foreign to a programmer. We `each`, `loop`  all the time (heh). The key is to realize that recursion with a base case is similar to iteration - it'll stop eventually - and that recursive functions get evaluated exactly the same as any other code.  
Visuals help and as always: 
###Understanding is reached by moving methodically in very tiny steps while replacing large complex chunks with smaller, digestible ones 
So let's do that!  
</br>

## Visuals, Examples, Graphs, Yay!

Here is some Ruby code for a real recursive function that computes the [Factorial](http://mathworld.wolfram.com/Factorial.html) of a number:

``` ruby

  def factorial(number)
    if number == 0
      1
    else
      number * factorial(number-1)
    end
  end
```


If you do `factorial(5)` you'll receive `120`.  
Uh, ok I guess that makes sense. But how?  

**WELL I'M GLAD YOU ASKED I'M SO EXCITED TO SHOW YOU!** (read on)

-----

Let's focus on this important line:  
`number * factorial(number-1)`  
When we pass `5` into the function, the first thing it hits is the `if` block. `5` is not equal to `0`, so we land in `else` - The important line I mentioned above. 

let's evaluate it from left to right, replacing `number` with its value, `5`...

`5 * (factorial(5-1))`  
and again evaluating further…  
`5 * (factorial(4))`

Well hold on now. `factorial(4)` needs it's own evaluation. Back to the important line above, when we pass `4` into `factorial(number)` we get:  
`4 * (factorial(4-1))`  
or  
`4 * factorial(3)`  

So now altogether we have something like:

`5 * ( 4 * factorial(3)) `

Likewise, continuing to evaluate the Ruby expression `factorial(3)` we arrive at:

`3 * factorial(2) `

Replacing the expression with this value in our running chain we get: 

`5 * ( 4 * ( 3 * factorial(2)))`

Following the trend of evaluation... 

`5 * ( 4 * ( 3 * ( 2 * factorial(1))))`

...and one more time:

`5 * ( 4 * ( 3 * ( 2 * ( 1 * factorial(0)))))`

Hang on, something is different now. Look back up to the full method. Evaluating `factorial(0)` will land us in the `if` rather than the `else` part of the block. This part returns the value `1`, *not* another call to the `factorial ` method! Let's replace that nice gentle number into our chain:

`5 * ( 4 * ( 3 * ( 2 * ( 1 * ( 1 )))))`

Every time we get a bundled-up expression rather than a nice, unpacked, *math-able* return value, we're going to continue interpreting and replacing until we end up with something upon which we can do arithmetic.   

## Interpret-O-Vision

This is a dense topic and it can never hurt to be **more clear** - *a small confusion will recursively grow larger with no base case in sight!* - so let's make it a little more visually-appealing.  
Here's stepping through `factorial(5)` like an interpreter..

```

factorial(5) => is 5 == 0 ? no. return 5 * factorial(4) 
    factorial(4) => is 4 == 0 ? no. return 4 * factorial(3)
        factorial(3) => is 3 == 0 ? no. return 3 * factorial(2)
            factorial(2) => is 2 == 0 ? no. return 2 * factorial(1)
                factorial(1) => is 1 == 0 ? no. return 1 * factorial(0)
                    factorial(0) => is 0 == 0 ? yes! return 1
                    finally, nothing else to evaluate. we landed on a number.
```
*(I'm going to beat this into your/our head/s)*

Now that we know that `factorial(0)` returns `1`, we can go up the stack and replace `factorial(0)` with `1`:

```
factorial(1) => return 1 * factorial(0) 
factorial(1) => return 1 * (1)
factorial(1) => return 1
```

Pop that back up a level in the Interpret-O-Vision, look for an expression for which you know the return value and substitute it...

```
factorial(2) => return 2 * factorial(1)
factorial(2) => return 2 * (1)
factorial(2) => return 2
```

Up a level again:

```
factorial(3) => return 3 * factorial(2)
factorial(3) => return 3 * (2)
factorial(3) => return 6
```

...

```
factorial(4) => return 4 * factorial(3)
factorial(4) => return 4 * (6)
factorial(4) => return 24
```

Last one!

```
factorial(5) => return 5 * factorial(4)
factorial(5) => return 5 * (24)
factorial(5) => return 120
```

And there we have it. `factorial(5)` returns `120` !

## "Did Somebody Order Dominoes?""

To really drive the point home in a beautiful pure number cascade. This is sort of what happens when the interpreter reaches the base case and can begin returning and *mathing* on values:

```
5 * ( 4 * ( 3 * ( 2 * ( 1 * ( 1 )))))   
5 * ( 4 * ( 3 * ( 2 * ( 1 * 1 )))))  
5 * ( 4 * ( 3 * ( 2 * ( 1 ))))
5 * ( 4 * ( 3 * ( 2 * 1 )))
5 * ( 4 * ( 3 * ( 2 )))
5 * ( 4 * ( 3 * 2 ))
5 * ( 4 * ( 6 ))
5 * ( 4 * 6 )
5 * ( 24 )
5 * 24
120
```

*It's beautiful*. When the interpreter can finally stop recursing and start returning, the big stack of self-similar calls falls back into itself like an imploding building. Finite recursion, while dense, is not entirely elusive. It's *infinite* recursion that is impossible to imagine (you think you're imagining it right now but you're merely imagining an infinitely small portion of it.)  


##Recursion is Fundamental to our Species
Maybe you're sitting there thinking,
> Duh… computers are stupid. This is boring. 

That's ok! Recursion is still a really cool concept and has connections to biology and other parts of the natural world. Do you think humans am stupid, too? [There](http://www.edge.org/conversation/recursion-and-human-thought) are [theories](http://press.princeton.edu/titles/9424.html) that recursion is an integral part of what elevates human cognitive abilities above other non-human animals.  
You can sort of see this yourself: ([solipsists](http://en.wikipedia.org/wiki/Solipsism), look away now) *I know that you're thinking and I know that you know that I know it.*  
What is that if not a self-similar repetition?! Don't take for granted the fact that you can imagine that very complex relationship with ease. I love my cat, but there's no way that he knows that I know that he's a cat. In his head it's all just like, *"cat cat cat cat cat"*.   
(I just tried to imagine his imagining without a base case to rescue me and almost got stuck in his head!)

It only takes a small stretch of imagination to entertain the idea that our ability to recursively model other minds is at the root of our capacity for *empathy*. That is **cool.**  
<br />

-----
\* *Ripping Spacetime*, pretty awesome speed metal band name?
 
