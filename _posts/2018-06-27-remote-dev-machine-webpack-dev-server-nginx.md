---
layout: post
title: "Using webpack-dev-server and HMR on a Remote Machine/VPS"
comments: true
excerpted: true
categories: how_to webpack vps front_end
description: How to get webpack-dev-server, HMR and livereloading working over nginx on a remote dev machine
keywords: webpack, webpack-dev-server, hmr, vps, javascript, nginx
---

_Setting up_ webpack-dev-server HMR on a remote machine to work over nginx isn't fun - but **USING IT IS!**

<!--more-->

**The Problem:** Using `webpack-dev-server`'s livereloading and HMR features on a remote machine (probably over nginx)

**<a href="#the-solution">The Solution</a>** is further down on this page for the impatient _(or those who very reasonably don't care to read about how I got into this situation and how long it took me to solve it!)_.

## The Fluffy Backstory

The joys of livereloading, hot module replacement, instant style updates and their related, rapid relatives have only recently come into focus for me. Now that I've seen this dazzling light the idea of toiling away in a dark alley of constantly `Ctrl-R`ing a browser window makes me <a href="javascript:void(0)" title="TODO: This will be a post about workflow 'friction'">very miserable</a>. I've recently adopted a workflow that involves working on a remote, hosted VPS over `SSH` in the terminal. I love almost all the <a href="javascript:void(0)" title="TODO: This will be a post about my dev VPS workflow">things about it</a>, but it briefly pushed me down the dark `Ctrl-R` alley. The main reason is simple: You're no longer hitting a `localhost:NNNN` page anymore - instead you're going out over the internet.

There are a few issues:

- On-Disk vs In-Memory builds of the site
- Hosts and DNS
- Ports (who uses which ports, who knows this, how to tell the various parties what's where)
- Firewalls
- Things about HTML headers
- Things about websockets

I spent hours and hours and purpled all google searches I could think of. sometimes after spiraling around I'd come back around to older google search results but this time I'd have a different set of configuration combinations as a result of walking through _previous_ google search results so I'd try some of these things mixed in with weird combinations of other stuff I'd already tried.  
It was one big shitty salad of port, host, webserver combinations.

By the end, the viable solution is, in summary, this:

- A publicly-accessible URL (let's call it `http://devenv.com`. and I already checked, it's taken) with DNS records pointing this domain to the IP of the VPS we're working off of.
- A static-built version of the files at `/dist`, served up by a simple nginx server block pointed to the static `index.html` when navigating to `http://devenv.com`.
- webpack-dev-server running, serving an in-memory version of the site over local port `8080`.
  - another nginx server block _using a subdomain such as_ `http://live-and-hmr.devenv.com` which proxies the websocket connection over to the above webpack-dev-server process on `8080`.

What I didn't understand originally was that webpack-dev-server **is a server** (duh) and as a result nginx should not be _doing the serving_ of that resource. It merely needs to step aside and hand off the responsibility to webpack-dev-server. This tripped me up, conceptually, before it clicked and prevented me from reasoning properly enough about the solution in order to arrive at it earlier.

One wouldn't have to use the two URLs (with and without the subdomain going to the static and dev-server versions) but I found it convenient to be able to work off the HMR dev-server version 90% of the time while keeping the convenience of building the site and flipping over to the static tab for a sort of more `productiony` experience.

I thought a bit about why there were so few Stack Overflow posts or blog article about this solution and I arrived at: The remote dev vps approach is relatively uncommon and it may be even less common among front end developers. This is a bit of an assumption and maybe a rude-ish one, but one which is grounded by this bias: Front-end-mostly devs are more likely to be spending their valuable time working on javascript/webpack/gulp/styling workflows, etc. - all of which are noble pursuits and beautiful, but its easy to spend much of your time in that world without having to worry about hosting details, nginx, processes/ports, and the like.  
To be clear, this is not a value judgement. Quite the contrary; being a mostly-back-end-developer myself I started off with very little knowledge on the front end challenges listed above and I have a lot of respect for those who know this stuff inside and out.  
It has been a long and rewarding journey for me.

<h2 id="the-solution">The Solution</h2>

Enough of my yakking! When I finally got the thing working I hastily noted it all down in a GitHub Gist (after doing a lot of wild, expletive-laced celebratory gesturing). The Gist will likely make enough sense to someone well-versed in webpack and its configuring, but I don't know that its the clearest thing. Let me know if you have questions.

- [Link to gist](https://gist.github.com/vcavallo/4f11985c4364bc4edfdf56556bff4ccf)
- Embed:
{% gist 4f11985c4364bc4edfdf56556bff4ccf %}

## Bonus for Rails + Webpacker users

There's another post forthcoming on Rails + Webpacker over VPS, but for now here's another hastily-written gist with the solution for that setup (warning: it's _weirder_):

- [Link to gist](https://gist.github.com/vcavallo/22cac63d01e3b73a56a92a619c6ff698)

----------

Questions, comments, concerns and ridicule all welcome below!
