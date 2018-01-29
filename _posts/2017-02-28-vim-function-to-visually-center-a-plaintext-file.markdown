---
layout: post
title: "How to center a pane in vim"
date: 2017-02-28 16:51
comments: true
categories: vim markdown how_to
excerpted: true
published: true
keywords: vim, centering, pane,
description: An easy way to visually-center a pane of prose in Vim
---

<style type="text/css"> /* Better styles for embedding GitHub Gists */
.line-data { font-size:11px; font-family: Consolas,"Liberation
Mono",Courier,monospace; } .line-numbers { font-size:11px; background-color:
#ECECEC; border-right: 1px solid red; color: #AAAAAA; padding: 0.0em;
text-align: right; } .line-pre { font-size:11px;font-family:
Consolas,"Liberation Mono",Courier,monospace; } </style>

Centering a vim pane within a full-screen terminal window is really nice when focusing on writing a single buffer of non-code prose. Here's how to do it.

![Centering animation](/images/vim-center-pane.gif)

<!--more-->

# How to center a pane in vim

## TL;DR:  

![Centering animation](/images/vim-center-pane.gif)

###[link to gist](https://gist.github.com/vcavallo/c3147fca261c78bd9c4a3648089b22e8#file-vim-centerpane)

The idea is to get the _content_ visually centered on the screen.  Typically
when I am writing non-code text I still use vim - because it's fantastic no
matter what you're doing with text - and in a fullscreen terminal, because
that's my workflow for everything. I like to keep to a sane margin width as
well. Once you are operating like that, it's natural to want the content
centered, rather than off to the left side of the screen.

![Centered pane target](/images/vim-center-target.png)  
(we want the white rectangle to appear in the area of the red one)

This is something that vim doesn't do on its own. There's probably a plugin for
it or something but I like to keep my plugins to a minimum, especially when
it's for something that the software can do entirely on its own without much
coercing.

## The solution

We can open up a new empty buffer in a vertical split using `:vnew`. This gets
us closer to moving our content around, but it'll start on the wrong side (the
empty split will open on the right). Using `:lefta vnew` will open the split
'left and above', which in the case of being the first split opened will just
put it to the left:

![Blank split](/images/vim-left-split.png)  

By controlling the width of this left pane we can get the content we're
interested in to the spot we want it:

![Resized split](/images/vim-left-split-smaller.png)

Manually creating a split and resizing it every time we want to center some
content like this is annoying, though. And the whole point of using a
programmable editor is to make it bend to our every whim with minimal effort.
Thus:

## Some vimscript

This happens to be my first vimscript function. I never needed to write one
until now. It has the benefit of being very simple:

<script src="https://gist.github.com/vcavallo/c3147fca261c78bd9c4a3648089b22e8.js"></script>

The three lines of the function:

- open a new split on the left (and automatically switch to it)
- switch back to the content pane
- resize the content pane to be 75% of the total screen

The last line of the above snippet just maps the function call to a key - in
this case, `Leader - c`. You'll likely need to adjust that mapping as well as
potentially change the resize amount based on how much spacing you want
(maybe you use a different margin than I).

**Huge disclaimer**: I haven't yet tested this on a screen size other than the
one I just wrote this function and post on... Might be completely broken
everywhere but this here laptop!

I'd be happy if any readers leave comments or scoldings on that gist. I'm sure
there are things wrong with it.  
Enjoy!
