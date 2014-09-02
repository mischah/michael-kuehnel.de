---
layout: post
lang: en_GB
title:  "„Welcome“ aka „This is the first post on my blog“"
date:   2014-09-01 21:53:08
category: blogging
tags: "blogging, jekyll"
excerpt: I’m starting blogging for the very first time on my own blog. This is something I had in my mind for ages. But I never managed to take the time setting up a blog (besides the legendary but long gone whuddupbro.com … but that’s a whole different story).
disqusIdentifier: 2014-09-01welcome-first-post
---

**It’s happening!**
I’m starting blogging for the very first time on my own blog. This is something I had in my mind for ages. But I never managed to take the time setting up a blog (besides the legendary but long gone [whuddupbro.com](http://whuddupbro.com) … but that’s a whole different story).

I started working on this blog in may for a couple of hours … zzzZZ ; ]  
But a few days ago I released version 1.0.0 of a little open source project called [Bootstrap Kickstart](https://github.com/micromata/bootstrap-kickstart)  :octocat: and I felt the strong need to let the world know about it (a Blog post will follow very soon). So I continued working on the blog and it is ready to be published **NOW**.

## Why?
I just love to share knowlege. Period.

## What’s happening over here?
We will see how much time I get to create epic articles for publishing them over here. So first of all I probably going to write tiny to medium sized posts every few days like a did on [gist.github.com/mischah](https://gist.github.com/mischah) once in a while.

### No link lists
But I don’t plan to make those link list articles in the style of „Hottest links of the week“. Because I guess there are enough (and awe-inspiring) sources already available. But you can follow me on [Twitter](http://twitter.com/mkuehnel) where I do post hot links from time to time.
Anyway, my personal recommendation if you like to get the finest selection of weekly links right into your inbox is the [Web Development Reading List](http://wdrl.info/) gathered by [@helloanselm](http://helloanselm.com/).

## Technical aspects
First things first: I didn’t want to use a blogging system with potential vulnerabilities („Hey WordPress“). So I could either use the legendary file based CMS [Kirby](http://getkirby.com/) (markdown #ftw) which will be released in Version 2 in September/October 2014 or make use of a static site generator.

Using Kirby meant that I still have to use a server side language (PHP in that case). So I decided to have a look at those ubiquitous static site generators.

### Choosing a static site generator
There are dozens of generators which let you compile static HTML files on your machine you can easily deploy to a simple server with minimum requirements afterwards. Most of them dealing with *markdown* files. So generating content is about editing plain text which is a delightful experience compared to the hassle with using one of those annoying WYSIWYG „Rich Text“ editors. Especially when your are used to write markdown for READMEs and Docs.

---

Yes, I had a look at those new and shiny generators from the *Node.js* world like [Metalsmith](http://www.metalsmith.io/), [Assemble ](http://assemble.io/) etc. 

Positive aspect: They are pretty handy to use and they’re coming with *Grunt* respectively *Gulp* based build tools which is awesome in case you already working with these kind of tools.

On the negative side these tools are that new, that I’m missing basic features like [pagination, navigation etc](http://assemble.io/plugins/#plugins-we-want).

---

## Enter Jekyll

Long story short → I’ve chosen the *Ruby* based **Jekyll** mainly out of the following reasons:

1.  Solid and widely used „product“ with a huge community.
1.  Incredibly easy to modify without using Ruby.  In fact  you don’t see any ruby code in your local installation.
1.  Used by Github pages which makes deployment easy as never before.

Let’s talk about deployment. In case your a using a Github repository called username.github.io it’s dead simple like pushing your master branch to that remote:

```bash
$ git push origin master
```

*#OMFG … that was easy!*

Checkout these docs ([Github](https://help.github.com/articles/using-jekyll-with-pages), [Jekyll](http://jekyllrb.com/docs/github-pages/)) if you like to get more info about using Jekyll in conjunction with Github.

The only thing I’m missing is a Grunt / Gulp based workflow by default. But there is a [Grunt task](https://github.com/dannygarcia/grunt-jekyll) available which I will integrate in my installation very soon.

You can checkout my Jekyll setup in a Github repository called [mischah.github.io](https://github.com/mischah/mischah.github.io)

There will be a follow up post describing a few key points on setting up Jekyll.

**Last words about the Jekyll community:**  
The maintainer and the community seems to be super friendly. I was happy about the communication as well as about the speed of merging my tiny [Pull request](https://github.com/jekyll/jekyll/pull/2862) regarding an iOS orientation issue within the default theme.

##tl;dr

I love to share my knowledge and doing this with the help of Jekyll and Github from now on. Enjoy my blog : ]





