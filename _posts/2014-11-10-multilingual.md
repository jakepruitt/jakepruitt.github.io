---
layout: post
title: Multilingual
image: /images/multilingual.jpg
description: The hardest part about learning programming is figuring out what to learn first. This article goes through all of the major programming languages, describes what each is good at, and gives you some good links to learn more.
---

![](/images/multilingual.jpg)

The hardest part about learning programming is often just the process of deciding which language to learn first. When making this decision, it's good to first know what each of the languages is like, what its applications are, and why you might want to learn it over other languages. Yesterday, I read a great article by Cecily Carver about [things she wished people had told her when she was learning to code](https://medium.com/@cecilycarver/things-i-wish-someone-had-told-me-when-i-was-learning-how-to-code-565fc9dcb329). Definitely worth the read. It got me thinking about the problem of "Not knowing what you don't know", which was my problem when I started out.

Hopefully this will help you get a better picture of what you don't know. We'll go from the origins of code to modern and future languages.

## Assembly Language - *Ancient Egyptian*

Assembly language is machine language, every single line directly corresponds to a 32 digit binary command that tells the processor which wires to give power and which to turn off. It's much like learning how to read hieroglyphics, since it is extremely different from the way people talk or think:

```R
addi	$a0, $a0, -1
jal		function1
move 	$s0, $v0
move	$s1, $v1

lw		$a0, 0($sp)	
addi 	$sp, $sp, 4	
lw		$ra, 0($sp)	
addi	$sp, $sp, 4	
```

That's just a few lines from a 150-line procedure for calculating [Fibonacci numbers](http://en.wikipedia.org/wiki/Fibonacci_number). I wrote it a few months ago, and I can't even tell you what it means.

### Why learn it

I'm pretty sure there are still a few people who use assembly to program drivers - the programs that allow hardware to interface with your computer. There are also a few game developers that occasionally dip their toes into assembly. The advantage of learning assembly is that you will have a very in-depth grasp of how a computer thinks and behaves.

### Getting started

Only attempt learning assembly if you are already confident with other programming languages and are curious about the way the hardware thinks. If you are ready to take it on (and have masochistic tendencies), you can look into these [free books on Assembly](http://resrc.io/list/10/list-of-free-programming-books/#assembly-language). Good luck.

## C/C++ - *Latin*

One level above assembly language is C and C++. You can think of C++ as "C with bonus features and behind the scenes content". They both operate very close to the machine level, and most heavy-duty software applications, including the inner workings of Node.js, the Chrome browser, operating systems, and high-powered PC video games are written in C or C++. All languages later in this article are evntually turned into C by some sort of compiler or virtual machine.

There are programmers out there who believe [you aren't a real programmer unless you know C pointers](http://www.joelonsoftware.com/articles/ThePerilsofJavaSchools.html). I personally find this approach very damaging to the community; you should never let someone tell you that you [aren't a "real" programmer](https://medium.com/@cecilycarver/things-i-wish-someone-had-told-me-when-i-was-learning-how-to-code-565fc9dcb329).

### Why learn it

Like assembly, learning C/C++ can really improve your knowledge of how computers work from the inside out. There is very little you will feel uncomfortable with after you master C++. I personally like C++ quite a bit due to its versatility and power. One day I hope to contribute to the Node.js core C++ code, so I will be trying to learn more of this once I finish mastering JavaScript.

### Getting started

If you are feeling brave, start by perusing the sources in [this stackoverflow question](http://stackoverflow.com/questions/388242/the-definitive-c-book-guide-and-list). Then, explore all of the other [free books on C](http://resrc.io/list/10/list-of-free-programming-books/#c) and [C++](http://resrc.io/list/10/list-of-free-programming-books/#c-1) available.

## Java - *French*

Java is a very well structured language, with very formal conventions and strict adherence to those rules. My coworker once described Java as a gun with lots of safeties. It has conventions and rules in place to prevent you from shooting yourself in the foot, but I sometimes find the structure is a bit stifling. Java has been around for a long time, and it still remains one of the most used server-side languages, although its old age sometimes makes it the punchline to a programmer joke about outdated languages.

### Why learn it

Since Java has a very structured approach, it can be useful for beginner developers to start with Java, learn the conventions, and carry those best practices over to other languages. Java is used to develop Android, so if you want to be building apps to one day ship to the Google Play store, Java would be very good to learn. Twitter's backend uses [Scala](http://www.scala-lang.org/), a very popular derivative of Java, so the language is definitely a good foundation to a lot of companies. Java was actually my first language (but I'm pretty happy I don't need to go back anytime soon).

### Learning resources

[Treehouse](http://teamtreehouse.com/features/android) offers a paid course on Android development, as well as a number of raw Java courses. You can also read through [this online book](http://introcs.cs.princeton.edu/java/home/) on Java basics, or look at all of these [other free books](http://resrc.io/list/10/list-of-free-programming-books/#java). I personally first learned programming by Oracle's [Java tutorial](https://docs.oracle.com/javase/tutorial/index.html). I would recommend you don't do that, it's not fun at all.

## JavaScript - *Creole*

JavaScript was kind of an accident created during the browser wars when Netscape was trying to push out features very quickly. Brendan Eich [created the language in 10 days](https://www.w3.org/community/webed/wiki/A_Short_History_of_JavaScript) in 1995. JavaScript should not be confused with Java, the name for JavaScript was actually chosen mostly as a marketing ploy because Java was very popular at the time. Due to its rushed nature, a lot of bad things were baked into the language, but there were also a large number of accidental [Good Parts](http://it-ebooks.info/book/274/).

### Why learn it

JavaScript is the native language of the web, whether people like it or not. It is quirky, but it is implemented in every modern browser, and nearly every modern page on the internet uses JavaScript, and web applications like Gmail are built almost entirely with it. As the web continues to be a growing part of the world we live in, JavaScript will continue to grow in importance. A lot of cool future web technologies, including [WebGL](http://www.chromeexperiments.com/webgl/), [WebRTC](http://www.webrtc.org/), and [Web Components](http://webcomponents.org/), will be using JavaScript as the primary interface.

JavaScript not only exists on the browser, but extends all the way to the server with [Node.js](http://nodejs.org/). There are also people looking to JavaScript to pave the way for the [Internet of Things](http://nodeup.com/seventythree). Oh, and did I mention [Paypal](https://www.paypal-engineering.com/2013/11/22/node-js-at-paypal/), [Netflix](http://www.infoworld.com/article/2610110/javascript/paypal-and-netflix-cozy-up-to-node-js.html) and [Walmart](http://venturebeat.com/2012/01/24/why-walmart-is-using-node-js/) use it as their back end?

If that's not enough to convince you, JavaScript has a really vibrant community that I [wrote about in a previous post](/2014/11/05/communal.html). It also is incredibly expressive as compared with the strict conventions of Java, as can be seen in this literary buff's take on [If Hemingway Wrote JavaScript](http://byfat.xxx/if-hemingway-wrote-javascript), one of my favorite books.

### Getting started

I will direct you to my earlier blog post about [learning to code with JavaScript](/2014/11/02/curriculum.html) if you are interested in learning it.

## PHP - *German*

[PHP](http://php.net/) has the unfortunate reputation of being a very ugly language to people who don't use it often. Even the name itself is upsetting. PHP stands for "**P**HP **H**ypertext **P**reprocessor". Yeah, the name is in the definition, it just keeps going on in an infinite loop. Now you understand the frustration.

### Why learn it

As bad as PHP's rep is, it is part of many of the most successful websites in the world. [Wordpress](https://wordpress.org/), the most popular content management system in the world, uses PHP. Facebook is built on PHP. If you want to be making web sites or applications that utilize great big databases, PHP may be the way for you to go, but not until you know HTML first.

### Getting started

Treehouse has great paid [PHP](http://teamtreehouse.com/library/topic:php) and [Wordpress](http://teamtreehouse.com/features/wordpress) courses. [Lynda.com](http://www.lynda.com/MySQL-tutorials/PHP-MySQL-Essential-Training/119003-2.html) also has good tutorials. The best way of all to learn PHP is to make your own Wordpress site!

## Ruby - *Japanese*

Ruby fans often describe Ruby as the most elegant of all programming languages. There are no ugly curly braces, everything is an object, and very powerful programs can be executed in a few Haiku-like lines. Some of my programming heroes are big ruby fans, including my past two bosses. I have used Ruby for class projects with the great framework [Ruby on Rails](http://rubyonrails.org/).

### Why learn it

If you want to become an in-demand web developer and hone your craft in a language that is tailor made for excellent programmers, that is what Ruby can offer you. [Github](https://github.com/), the social network for developers, is built with Ruby. That being said, I've often found the Ruby community to not be as open and accepting of beginner programmers as Node.js. The Ruby learning path is very much based on learning eloquent code, and the language can be unforgiving to beginners. Also, many Ruby tools do not work well on the Windows operating system, so if you want to be serious, you should have a Mac or Linux machine.

### Getting started

Check out the beginner resources at [Try Ruby](http://tryruby.org/levels/1/challenges/0), [RubyMonk](https://rubymonk.com/), and the very good [Ruby Koans](http://rubykoans.com/). You can also learn through paid courses at Treehouse, or read free books as listed on [reSRC.io](http://resrc.io/list/10/list-of-free-programming-books/#ruby).

## Python - *English*

[Python](https://www.python.org/) is widely regarded as the most English-like language of all of the programming languages. The syntax flows like a sentence, and just about anyone could figure out what a Python program is saying. Take a look at the almost-English 7 line function for Fibonacci numbers:

```Python
def fib(n):
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()
fib(1000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
```
The language's name comes from "Monty Python's Flying Circus", and has a number of Monty Python hidden jokes. Python is a great general purpose language with a great community and tons of learning resources.

### Why learn it

Python has a very wide application, and is used very frequently in the world of finance, physics simulation, web data transfer protocol, and operating system interfaces. If I were to recommend someone to start learning how to code today, I would probably recommend Python.

### Getting started

The best place to start is the [Python FAQ](https://docs.python.org/3/faq/general.html#what-is-python), which has great explanations of the language and programming in general. If you learn well from books, check out these [free Python books](http://pythonbooks.revolunet.com/). Also check out the [Python tutorial](https://docs.python.org/3/tutorial/index.html#tutorial-index).

## Bonus: LISP family - *Khoisan Languages*

Do you remember seeing a clip on National Geographic of African tribes speaking in a clicking language? And it sounded nothing like any other language you heard before?

Yeah, that's the LISP family in programming.

[Clojure](http://en.wikipedia.org/wiki/Clojure), [Scheme](http://en.wikipedia.org/wiki/Scheme_(programming_language)), and their cousin [Haskell](https://www.haskell.org/haskellwiki/Haskell) are all functional programming languages, and behave fundamentally differently from typical programming languages like C and Java. I personally find them very beautiful, and will be trying out [ClojureScript](https://github.com/clojure/clojurescript) in the near future.

## One ecosystem

All in all, no matter if you are a hard-core C programmer, a casual Pythonista, or even a LISPer, all programmers have one thing in common: They all love to learn, and spend their lives dedicated to lifelong learning.

I hope I did not ruffle anyone's feathers too badly in my descriptions of these languages from my limited experience. If you have any recommendations for other reading sources or corrections to my descriptions, please let me know in the comments below or on Twitter [@thejakepruitt](http://twitter.com/thejakepruitt).
