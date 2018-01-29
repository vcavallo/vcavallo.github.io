---
layout: post
title: "A Way To Share Bash Scripts Between Machines"
date: 2015-08-29 13:30
comments: true
categories: bash git scripts environments
excerpted: true
published: true
keywords: bash, dotfiles, scripts
description: Sharing command-line scripts across different development machines
---

Or: How I thought I invented the "dotfiles" and "scripts" repo idea... Read on if you like having access to the same command-line tools on different machines.

<!--more-->

# Scripts that get around

_I couldn't think of a better title, but infinite second-guessing is what has kept this 
blog update-less for two years. No more._

## Making computers do stuff I want

I've recently been expanding my knowledge of Bash and the *NIX system in general[^1]. It 
has been extremely rewarding both as an intellectual hobby and in terms of increasing 
my productivity and lower-level understanding of what exactly is going on under the hood 
when I'm doing ...well _anything_ on a computer. In any creative or intellectual field 
composed of an array of siloed information - a horizontal of verticals - the deeper down 
you can get into the most number of verticals, the more useful your creative contribution 
will be / the better you'll understand the overall topic. 
[This excellent Wait But Why post](http://waitbutwhy.com/2015/06/how-tesla-will-change-your-life.html) 
discusses this general concept quite a bit in the beginning and it really spoke to me. 
I recommend you listen to it so it can speak to you also.  

But I'm seriously digressing. This post is about how I set up some super simple and fun 
Bash scripts in concert in order to solve an actual problem I often have:  

> **I want to able to do certain minor custom command-line things on a number of different computers.**

The tasks are simple: things like "open up vim inside a certain directory" or "transform 
some string on my clipboard" - super easy stuff that doesn't necessarily warrant an afternoon 
of experimenting and blog-post-writing. But now I have a framework for myself to expand 
upon, plus I learned some cool stuff along the way (I purposefully didn't search Google 
for a preexisting solution, which I am _sure_ exists since I already use 
[something similar for dotfiles](http://blog.smalleycreative.com/tutorials/using-git-and-github-to-manage-your-dotfiles/))

## A github repo for you

**[Here is the repo I made](https://github.com/vcavallo/scripts)**. The bones of it are 
as follows:  

- `readme.md` - duh.
- `install.sh` - this installs the scripts for you so you can use them right away.
- `directory and files` example files - these serve as instructions. explained in readme.
- the actual bash scripts.

The general idea is that the installer makes scripts executable and symlinks in a 
place in your PATH, getting its relevant information from the `directory` and `files` 
in order to be flexible and environment-semi-agnostic.  

There are many things I should change[^2], so this blog post might quicky be reflective 
of some past version of the repo rather than the present version you see but I'm sure 
the general idea will hold true.

## Serious things I learned:

- The `~` character gets expanded by Bash. This can make weird things happen if you're unsure 
    how you're using the `~` in different parts of your script. I kept getting unknown 
    file or directory errors on `~/scripts` when I was working on the `chmod a+x` part. 
    It was _extremely_ confusing! which brings me to...
- `-xv` is your best friend. Appending it like: `#! /bin/bash -xv` will activate debugging 
    and verbose output. Using that I was able to see the very important single quotes 
    in this output: `chmod a+x '~/scripts/testing-executable'`. Since the tilde there is 
    part of a literal string, Bash wasn't expanding it to `$HOME` like I needed it to. 
    The NON-`-xv` version of the output was simply: `chmod: ~/scripts/testing-executable: No such file or directory` 
    which I unfortunately could not make sense of for a little while :)

### Comments, suggestions? Send me a tweet or email or pull request or postcard!

[^1]: I highly recommend this site to start off: [linuxcommand.org](http://linuxcommand.org/)
[^2]: a big obvious one that somehow only ocurred to me now is to put the scripts in a _folder_. jesus.



