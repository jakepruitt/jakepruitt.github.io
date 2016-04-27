---
layout: post
image: /images/compiling.jpg
description: Trying to empathize with the most CPU intensive work I have made my computer do in a while - bootstrap gcc.

---

![](/images/compiling.jpg)

My keyboard is almost on fire. I'm not sitting in the sun or typing incredibly fast. I'm putting my computer under a lot of strain in order to bootstrap my [gcc compiler](https://gcc.gnu.org/), and if you're anything like me, you have no idea what this means. Since I've been here watching this silent process for over half an hour, I figured I should sit down and try to understand what is going on, even if it won't make my computer any cooler or the process finish any sooner.

My other reason for doing this is that I eventually want to talk about pointers in C++, and it makes sense (at least to me) that I should start with the bare bones. There's this quote [from Carl Sagan](https://www.youtube.com/watch?v=7s664NsLeFM) that goes:

> "If you wish to make an apple pie from scratch, you must first invent the universe."

I'm not here to invent the universe. I'm definitely not here to teach you how to write a bootstrapping compiler. There are some incredibly smart people out there that know how to do this, and I am not one of them.

I'm just a kid staying up late wasting too much time reading articles about compilers, and this is what I can say about it.

## A list of words, one at a time

The first thing that might help us understand this whole universe better is a list of words, each defined by themselves, that we'll use a lot from now on:

- **Central Processing Unit (CPU)** - this is a small piece of hardware on your computer that takes instructions for saving, calculating, and moving numbers around. Inside of this black box is actually pretty straightforward - there are parts for arithmetic, parts for logic, parts for storing and retrieving data from short term or long term memory, and a few external wires that allow it to send instructions to other parts of your computer, like screens or wifi cards or speakers. If you ever have time to see what goes on inside a microprocessor (another name for CPU), definitely do. The important thing for us to remember is that it's hardware that takes instructions in the form of numbers. There are many different CPU's made by tons of different companies, each with their own unique instruction sets and internal mechanics. All programs that run on your computer eventually turned into instructions the CPU can understand.
- **Binary executable** - remember how I said the instructions are numbers? Well, a set of those numbers written all together in a long binary file is an executable binary file. These files are usually specific to their target CPU (since each CPU takes different instructions) and are fed, instruction by instruction, into the CPU for processing and execution. Now, humans can't read these files, since humans don't read long strings of binary. Which is why we have code.
- **Code** - for our purposes, I'll say that code is text files written by humans, readable by humans, that tells computers what to do. I'm sure there are plenty of people that have problems with this, and in some places this definition would be quite contentious. By this definition, Excell macros count as code, JavaScript counts as code, HTML and CSS count as code, just as much as C++ or FORTRAN. If you have a better definition, let me know, but the cutoff is inherently subjective, and surprisingly blurry. For the sake of this article, I'm going to take an intentionally broad definition.

Now that we have those words, we can start talking about the main purpose of this article - the way that code becomes CPU instructions.
