---
layout: post
title: Fundamentals
image: /images/stick-and-stones.jpg
description: Ever wonder exactly what programming is? In this article, we re-examine the basic fundamentals of code, and introduce the idea of an interface.
---

![Fundamentals - JavaScript Jake](/images/stick-and-stones.jpg)

*Before you start reading this post, it might be a good idea to read through the [tutorial](/2014/11/03/your-first-tool.html) for getting Node.js on your computer. Or, if you'd rather use an online playground, check out [JS Bin](http://jsbin.com/?js,console).*

When I started coding, no one ever explained to me what programming actually was. As far as I was concerned, programmers were wizards that drew messy diagrams on whiteboards, spoke secret parseltongue to computers, and then made Facebook appear. I was under the impression that it took four years of college in an intense Computer Science department to become a good programmer, and that I didn't have the time, patience, or knowledge to look under the hood of the black box on my desk.

This post is about the very fundamentals of programming, what code is, and what it means to write a program. By the end of this post, hopefully some of that mystery of code will be dispelled for you. If you are already familiar with programming, it's always a good idea to go back to basics and rethink the core of what you are doing. I'd love to know your ideas about programming in general, and what concepts you think are most important in working with computers.

This is how I see the black box of code.

## The Interface

The word **Interface** is one of those terms that gets thrown around a lot in computing, design, and physics as well. For the longest time, I just smiled and nodded when people used this word, but I never really understood the concept. It's a difficult concept, but once I understood it, everything seemed to click for me.

I once saw a video where a designer described an interface as a boundary, like the surface of a lake where water meets air. This idea still resonates with me. The air doesn't interact with anything under the surface of the water, it only has contact with that outermost layer.

An interface is any boundary, any layer that affords interaction between two things, like the words of a book or the screen of your TV. The verb **to interface** describes the action of two peices clicking together, each piece being made to fit with the other peice. It's the moment of the circus act where the two trapeze artists link arms in mid-air, they each had to practice and provide a way for the other trapeze artist to easily connect with them.

Hopefully these analogies help clear up what an interface is conceptually. Once it clicks for you, you will see that everything has an interface. The key to understanding programming is to think of it in terms of an interface.

## Below the Surface

Your computer is effectively a collection of a lot of pieces of hardware; hardware that can add numbers, perform logic, remember numbers, and send and receive numbers. That's about it, fundamentally. What makes a computer really really great is the interface it gives us to do those operations. Like the surface of the lake, all we see is the screen of pixels, and all we can do is move our mouse and type in the keyboard. The metal pieces and parts with electricity flowing through them are hidden away from us. When we want to access facebook, we can just click on icons, type in URL bars, and look at pictures of our friends. We don't have to manually turn on and off electricity to metal wires and then decode what the electrical response is.

We can happily be ignorant of what lies under the surface of our computer, and trust the thousands of brilliant people who have built the easy interface of screens and keyboards.

Code, just like the Facebook homepage in your browser or the image editing tool on your desktop, is an interface. It is a way to interact with your hardware at a lower level than clicking on buttons on a screen. With code, you have closer access to the memory, processor and networking hardware that lies within your machine.

If you wanted to tell your processor to add `2 + 2`, you could open up the calculator application and push the `2`, `+`, `2` and `=` buttons in that order, and it would show you `4`. Internally, the calculator application is just a bunch of presentation code that displays the application on the screen, reads the input from the user, and then, through the interface of code, tells the processor to add `2 + 2`, and displays the result. The person who wrote the code for the calculator didn't have to set up the wiring to add binary representations of 2 and 2. By writing code in text files in a way that the computer can understand, the developer had access to that hardware. Code is nothing more than another layer, the user interfaces with the application code, and the application code interfaces with the hardware. Think of code as translating clicks into hardware commands.

## Rethinking Fundamentals

With this in mind, you can now rethink what it means to be a programmer. Variables, mathematical and logical operations, graphical output, and network data transfer are all just the textual interfaces with the underlying hardware. The power of code is in its ability to abstract these basic components and use them to do powerful things. As a User Interface developer at [LaneTerralever](http://www.laneterralever.com/), my job is to utilize HTML code to give users a better interface. Without the code I write, people would see streams of unintelligible data from servers. I interface with the browser's languages to tell it how to show the response.

## Try it yourself

Want to try out some of these ideas on your own? With JavaScript (either in the [Node.js](http://nodejs.org/) REPL or in the [JS Bin](http://jsbin.com/?console) console), you can:

* Access memory with `var` (e.g. `var age = 13` stores the number `13` to the key `age`).
* Perform mathematical operations (e.g. `+`, `-`, `>`, or `Math.sqrt()`)
* Display information on the screen (e.g. `console.log("Hello World!")`)
* Send and recieve data (e.g. `http.createServer(...)` read more [here](http://book.mixu.net/node/ch10.html))

## Learn more

Here are some sources to start learning a little more about the very basics of programming in JavaScript:

* The introduction of [Eloquent JavaScript](http://eloquentjavascript.net/00_intro.html)
* Code Academy's free [JavaScript](http://www.codecademy.com/tracks/javascript) course
* Node School's [javascripting](http://nodeschool.io/) lesson (pro tip: type `npm install -g javascripting` in the command line, then type `javascripting` to begin the lesson)

Have fun and good luck! Let me know how you liked the post!