---
layout: post
image: /images/forethought.jpg
title: Forethought
description: There is just a tremendous amount of craftsmanship in between a great idea and a great product - Steve Jobs
---

![](/images/forethought.jpg)

There is no one perfect way to plan a project. Every project has a different situation, no project will pan out exactly as expected, and bugs are a fact of life, no matter how perfect you are. I've recently been given an exciting open source project to work on from my very smart friends at [nearForm](http://www.nearform.com/). I have about 8-12 weeks to create a checklist web app using the latest beta version of [Seneca](http://senecajs.org/), a micro-services toolkit for Node.js. I cannot wait to get started, and have tons of ideas floating around on where to begin.

But before I even begin, I want to work through a few thoughts that will help decide course of the project. I want to figure out my workflow, decide on the drivers of the project, and identify industry best-practices I want to incorporate into the design and management of my time. I have had a lot of projects go wrong before, and the following items are some ideas that I think can help ensure this project turns out great.

## 1. Requirements first

I want to focus a lot of my time at the outset of the project really understanding the exact requirements, and thinking carefully about the solutions. This may sound like a no-brainer: of course you should think about what you're building before you build it. However, a lot of my past projects have suffered from writing too much code before I truly understood the project. I've had to re-factor a lot of this code later in the project, sometimes re-writing entire parts of the codebase.

There are schools of thought that say code can always be rewritten, and the best approach for any project is to get rubber to road as soon as possible. However, I think that it is less expensive to change a mental model of a program when there is no code written, so I will make sure I at least have a good idea of what I am doing before any code is written.

## 2. Consistency

One of my primary weaknesses is consistently sticking with a project even after it stops being fun. I am very eager to start projects, but less eager about seeing them through to completion. This inconsistency has been the death of many of my side projects and has hurt me in school projects.

I really like the rhythm of the release cycles for Chrome and Ember.js, which consists of a new stable release every 6 weeks with a corresponding beta release for the upcoming version. This release cycle is [well documented by Ember.js](http://emberjs.com/blog/2013/09/06/new-ember-release-process.html), and described fully in an episode of [the changelog podcast](http://thechangelog.com/131/). Just like holding myself to a daily rhythm of blog post writing has forced me to be consistent, I think holding myself to a strict release cycle from the very beginning of the project will ensure that I consistently deliver throughout the life of the project. I will be trying to get a beta release within the first 4-6 weeks, which will be tested and refactored until it is ready for a stable release.

## 3. Functional Testing

I come from a functional testing background, and know just how effective it is at finding hidden bugs. Writing functional tests also helps me wrap my mind around the requirements, thus helping my first objective. I historically have written tests based on the code, rather than basing the code off of the tests. I will try to change that this time, and let the tests robustly test the functionality before any code is written, and force my code to be that robust.

I know functionality testing in the browser is a bit tricky right now with Node.js. I have had good experiences with [Capybara](http://jnicklas.github.io/capybara/) from the Ruby community, and may be willing to write tests in that as a last resort. For now, after listening to an episode about testing on the [NodeUp podcast](http://nodeup.com/seventyseven), it sounds like the best tools for testing in the browser is a combination of [Zuul](https://github.com/defunctzombie/zuul) for driving browsers with JavaScript, and [tape](https://github.com/substack/tape) for a minimal testing framework. Since [AngularJS](https://angularjs.org/) may play a role in the front end, there may also be a need for using [Karma](https://karma-runner.github.io/0.8/index.html) or [Protractor](http://angular.github.io/protractor/#/). I'll probably try to stick with the simplest solution to begin with.

## 4. Think small

Since things are bound to change from the beginning of the project to the end, I will try to design for that change from the very beginning. That is why I am using micro-services and [Seneca](http://senecajs.org/), since it is much easier to find and fix a problem when the modules of a program are small and single-purposed. From the very beginning of the architecture design, if any single element of the project becomes too complex, I figure out how it can be broken up into smaller pieces. I think this will be the hardest part for me, since I am still getting used to the architecture and design patterns of creating single-page web applications. Luckily, I can base many micro-service best practices off of the [seneca-mvp](https://github.com/rjrodger/seneca-mvp) example project. I also really enjoyed reading [Single page apps in depth](http://singlepageappbook.com/), which geared me toward having small views and minimal controllers.

So those are my top four priorities before any code is written. What kinds of considerations would you have if you were starting a single-page web app today? What would your priorities be? Let me know in the comments below or on Twitter!
