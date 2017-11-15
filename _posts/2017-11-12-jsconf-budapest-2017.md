---
layout: post
lang: en_GB
title:  "JSConf Budapest 2017 – A personal recap"
date:   2017-11-12 22:00:00
category: conferences
tags: "Conferences, JSconf Budapest"
image: "/assets/img/jsconfbp2017/family-photo.jpg"
excerpt: "It was my first time attending JSConf Budapest. In this recap I’ll summarize and highlight a few talks and try to convey the overall experience. TL;DR: It was a blast. Thanks to everyone involved :sparkling_heart:"
disqusIdentifier: 2017-11-12-jsconf-budapest-2017
---

<div class="float-container">
    <img src="{{page.image}}" alt="" class="float-left">
    <div>
        <p>
          {{page.excerpt}}
        </p>
    </div>
</div>


## General remarks

JSConf Budapest is – besides JSConf EU (The first JSConf in europe) and JSConf Belgium – another JSConf happening at the european continent which actually took place for the third time and therefore already has a tradition to one's name.

For those who don’t know the concept of the whole JSConf thing I’d like to proceed with a short explanation.

The [JSConfs](http://jsconf.com) happening around the globe are all community driven by heart. From the local community for the world-wide community. So there isn’t something like a huge common organizer behind all that conferences. But they do have something in common: All local organizers are focusing on the community aspect instead of being only tech driven. This is achieved by offering many possibilities for social interactions from lounges through open discussion panels to interactive games during evening events. All of that considering a code of conduct which is not only written somewhere on the conferences website, but also will be lived and enforced.

Another important fact is that the organizers set a high value on diversity concerning the speakers as well as the attendees. They offer diversity support tickets for example. The additional charge is used to give members of underrepresented groups the possibility to attend the conference.

The 2017 edition was the first JSConf Budapest for me after visiting JSConf EU in Berlin a while ago. I was very thrilled about Budapest accordingly.

## The location

The event location was a historic cinema in the heart of the jewish quarter in the center of the city. A monumental location. The only thing I kinda missed were more places to chill. 

## The schedule

It was a two day, single track conference. So there was no need to be afraid of choosing the wrong track and miss a talk :smirk:

The mixture of talks really was to my taste. The technical ones were predominating and there were very interesting talks which aren’t focused to technical details but enlightened human parts of our work life.

### Personal highlights of the non-technical talks

I’d like summarize and highlight the following three talks.

####  [Bodil Stokke](https://twitter.com/bodil) – You Have Nothing to Lose but Your Chains

The topic of this [talk](https://bodil.lol/join-us-now/#0) was Open Source Software. From their beginnings, through licenses to todays relevance. Whether you interpret Open Source and the Free Software movement as socialism, pragmatism or art: The idea itself and spreading is as important as it ever was. Then it has the ability to empower us. Making source code available to the general public doesn’t only mean that we can take influence, can fix and can improve software. It builds communities of developers and user which weren’t imaginable. First and foremost it enables us to learn.

![](/assets/img/jsconfbp2017/oss.jpg)

#### [Vaidehi Joshi](https://twitter.com/vaidehijoshi) – Goldilocks and the three Code Reviews

This [talk](http://slides.com/vaidehijoshi/better-code-reviews#/) illustrated problems we have with code reviews wrapped in an entertaining story. Including:

* tons of comments, little conversation
* focusing on style / syntax
* ego over empathy

Plus it showed concrete opportunities for action to fix these problems:

* review everyone: push for a culture that values vulnerability
* develop empathy: call out the good stuff, too!
* iterate: only iteration can improve the process
* start the conversation

![](/assets/img/jsconfbp2017/reviews.jpg)

#### [Madeleine Neumann](https://twitter.com/maggysche) – Impostor syndrome - am I suffering enough to talk about it?

in this important psychological talk Madeleine told her personal story of career development in which the [Impostor Syndrome](https://medium.com/@Maggysche/impostor-syndrome-am-i-suffering-enough-to-write-about-it-5de8074f2c60) acts a part.
My main take away from the talk was that everyone has moments of suffering from self-doubts from time to time. Lastly Madeleine gave very useful tips about how to get out of the impostor zone. See [slides](https://www.slideshare.net/MadeleineNeumann/jsconf-budapest-impostor-syndrome-am-i-suffering-enough-to-talk-about-it).

### Personal highlights of the technical talks

The following talks impressed me the most from the technical standpoint.

#### [Stefan Judis](https://twitter.com/stefanjudis) – Watch your back, Browser! You're being observed

A [roundtrip](https://speakerdeck.com/stefanjudis/watch-your-back-browser-youre-being-observed) across modern JavaScript web APIs which turns the way to gather information upside down. The concept of communications of older APIs mostly was based on a pull principle. Broadly speaking, you had to ask for information your are interested in. It seems that this has changed to an push principle with modern APIs.

Shortly explained using the example of the pretty new [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API): This API offers the possibility to listen if a DOM node gets in the visible viewport and to asynchronously get notified in case this happens.

The most prominent use cases are probably lazy loading images and implement infinite scrolling as an alternative to a classical pagination. We were of course able to implement these things before, but less performant and elegantly.

#### [Jonathan Martin](https://twitter.com/nybblr) – Async patterns to scale your multicore JavaScript … elegantly.

An excellent [talk](https://speakerdeck.com/nybblr/async-patterns-to-scale-your-multicore-javascript-dot-dot-dot-elegantly) about patterns to grasp the challenges when it comes to handle concurrency with sequential dependencies via JavaScript. Since the JavaScript interpreter in the browser and in Node is a single thread classical multithreading approaches don’t fit in here. But JavaScript and the underlying architecture based on the event loop, the call stack and the callback queue is a perfect match for concurrent programming. 

Jonathan came with recipes based on »Async IIFEs«, »Web Worker clusters« und »SharedArrayBuffers« to solve the concurrency challenges elegantly.

![](/assets/img/jsconfbp2017/concurrency.jpg)

#### [Eirik Vullum](https://twitter.com/eiriklv) – JavaScript Metaprogramming - ES6 Proxy Use and Abuse

An interesting talk providing real world use cases for one of the few non-polyfillable / non-transpilable ES6 features which you can use in in the latest browsers and Node.js versions.

A short explanation of proxies: JavaScript Proxies enables you to modify and extend fundamental language features (e.g. property lookup, assignment, enumeration, function invocation, etc).

Beside quite useful mini examples like auto-logging of object keys when accessing object properties I really was impressed by an Oprn Source project from Eirik: [JSON-populate](https://github.com/eiriklv/json-populate), which simplifies accessing JSON properties with circular dependencies by reference.

### Parties :tada:

A very special highlight was the party after the first day of the conference. Mainly because [{Live : JS}](http://livejs.network/) had a truly amazing live gig. They performed music running on two Gameboy Advance and did bedazzling live visuals exclusively based on web technologies. Mad props to Ruth, Tim, Sam und Martin. These folks truly rocked the party.

## Bottom line

Beside the talks (and the party) I especially was delighted by the social aspects of this conference attendance. It was a pleasure to see friends who I only have the chance to meet them once a year (beside hanging out with them online), as well as meeting new people who I knew before from Twitter only. 

Thanks to all the people for the nice conversations and your openness :sparkling_heart: Thanks to the folks for organizing JSConf Budapest :sparkling_heart: And thanks to my employer [Micromata](https://www.micromata.de/) for making it possible to attend JSConf Budapest :sparkling_heart:
