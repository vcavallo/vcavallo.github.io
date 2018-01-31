---
layout: post
title: "Setting up Middleman and Tailwind CSS"
date: 2017-12-06 16:16
comments: true
excerpted: true
categories: css static_site_generator how_to
published: true
keywords: middleman, tailwind, css, webpack, heroku
description: How to set up Middleman and Tailwindcss and deploy to Heroku
---

Middleman and Tailwind make landing pages a breeze (get it?). Here's how to get them to work together!

<!--more-->

I'm a big fan of the [Middleman](https://middlemanapp.com/) static site generator and static sites / markdown blogs in general:

- My consultancy's site, [exnil.io](http://exnil.io) is built on Middleman.
- [My personal blog](http://blog.vinneycavallo.com/) is built on [Jekyll](https://jekyllrb.com/) - a sort of cousin to Middleman.
- And this site you're reading is [Octopress](http://octopress.org/), a kinda defunct Jekyll nephew. (used to be Octopress... Migrated to Jekyll in 2018)


Lately I've been drinking the **utility-first CSS** kool-aid with glee. As others before me have also noted, [Adam Wathan's blog post](https://adamwathan.me/css-utility-classes-and-separation-of-concerns/) makes the argument quite well, so I won't get into my reasons here. Since I just mentioned Adam, it won't be a surprise that my utility-centric CSS framework of choice at the moment is [Tailwind CSS](https://tailwindcss.com/), which he co-created (or "_is currently co-creating_" since they are currently hard at work on the road to 1.0. And really when can the creation of any piece of software be in the _past tense_?)

I set out to build a pre-launch landing page for a new web app idea for which I am attempting to take a community pulse. I'm tentatively calling it [Rate my Refactor](http://www.ratemyrefactor.com) and the point of it is to facilitate discussion and advice around specific instances of refactoring and code quality. 

![Rate my Refactor screenshot](/images/rmr-screenshot.png)

The speed and friction-reduction afforded by both Tailwind and Middleman make their team-up a natural choice for a simple landing page. In an effort to hit the ground running I popped over to Google to find some direction on getting Middleman, Webpack, PostCSS and Tailwind to all play nicely together. (disclaimer, I'm traditionally a back-end developer so the unholy union of `npm/yarn/webpack/gulp/js/postcss/etc/etc` doesn't just come naturally to my fingertips.)  


I found a whole lot of nothing Googling around for this. Probably because most front-end devs come out of the womb knowing their way around yarn balls, gulps, and webby packs - but as I said, that's not me. Apparently I'm not alone: [http://www.impostorroster.com/posts/cannot-understand-how-webpack-works](http://www.impostorroster.com/posts/cannot-understand-how-webpack-works).


So I figure there's gotta be someone else out there looking for this answer.  
Hello, someone! Here it is:

# Show Me How To Do It Already!

[Here's a GitHub repo all set up for you](https://github.com/vcavallo/middleman-and-tailwind). These are the main bits:

- Middleman settings:
  - the `activate :external_pipeline` line in `config.rb`
- Webpack setup:
  - settings for js and css in `webpack.config.js`
  - the contents of `package.json`
- Tailwind config:
  - `postcss.config.js`
  - `tailwind.js` (generated as directed in their installation docs)

As an added bonus, this repo also has the configs necessary for an easy Heroku deploy.

# The Final Product...

I invite you to check out [Rate my Refactor](http://www.ratemyrefactor.com) for an example of a basic Middleman+Tailwind+Heroku site. Since you're reading a programming blog you probably care at least a little about refactoring - so why not sign up for the email list while you're over there?!

Thanks! If you have any improvements or problems please drop them in the comments below.
