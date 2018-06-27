---
layout: post
title: remote dev machine webpack-dev-server nginx
---

**The Problem:** Using `webpack-dev-server`'s livereloading and HMR features on a remote machine (probably over nginx)

**<a href="#the-solution">The Solution</a>** is further down on this page for the impatient _(or those who very reasonably don't care to read about how I got into this situation and how long it took me to solve it!)_.

## The Fluffy Backstory

The joys of livereloading, hot module replacement, instant style updates and their related, rapid relatives have only recently come into focus for me. Now that I've seen this dazzling light the idea of toiling away in a dark alley of constantly `Ctrl-R`ing a browser window makes me <a href="javascript:void(0)" title="TODO: This will be a post about workflow 'friction'">very miserable</a>. I've recently adopted a workflow that involves working on a remote, hosted VPS over `SSH` in the terminal. I love almost all the <a href="javascript:void(0)" title="TODO: This will be a post about my dev VPS workflow">things about it</a>, but it briefly pushed me down the dark `Ctrl-R` alley. Remedy below.



I spent hours and hours and purpled all google searches I could think of. sometimes after spiraling around I'd come back around to the same google searches but this time I'd have a different working situation as a result of walking through _other_ google search results so I'd try some of these things mixed in with weird combinations of other stuff I'd already tried. A salad of port, host, webserver combinations.  
I think the remote dev vps approach is relatively uncommon and even less common among front end developers who are mostly lurking around javascript and webpack stack overflow answers.

<h2 id="the-solution">The Solution</h2>

This gist has the instructions: https://gist.github.com/vcavallo/4f11985c4364bc4edfdf56556bff4ccf

The satisfaction of finally getting it working is hugely rewarding.

Another post needed about the Rails + Webpacker solution. here's the gist for that: https://gist.github.com/vcavallo/22cac63d01e3b73a56a92a619c6ff698



