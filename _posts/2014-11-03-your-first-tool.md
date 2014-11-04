---
layout: post
title: Your First Tool - The Node Command
image: /images/oIpwxeeSPy1cnwYpqJ1w_Dufer%20Collateral%20test.jpg
---

![](/images/oIpwxeeSPy1cnwYpqJ1w_Dufer%20Collateral%20test.jpg)

There is a lot to be said for simple tools. Things like spoons and knives have existed for thousands of years, and will always be effective. Pens, pencils and paintbrushes can give us hours of entertainment, and are so simple that anyone can at least doodle. Here we will be exploring the most simple [Node.js](http://nodejs.org/) tool, the `node` command. The `node` command gives you access to a playground to try out all that Node.js has to offer. It also allows you to execute JavaScript files on the command line! This may sound trivial, but it is the entire reason Node.js exists. Server-side JavaScript would not be possible without the `node` command, and you will use it in every Node.js program you write from now on.

## Getting Node.js

If you don't have Node.js installed, head over to the [download](http://nodejs.org/download/) page. There are plenty of installers available for Windows, Mac OS X and Linux. It's free to download and free to use on your computer. If you're not too familiar, Node.js is a server-side JavaScript platform. I chose it not only because I know JavaScript better than other languages, but because it is very easy to get up and running, and translates well into learning other languages.

Once you have Node.js installed, double-check that it is properly installed by opening up a console. This is done differently on Mac OS X and Windows. On Mac OS X, the application you need to open is called "Terminal".  It can be found under Utilities in the Application launcher. On Windows, click the home button and search for "Command Prompt". You should now have a blank window with a blinking cursor waiting for you to type. Go ahead and type

```
node --version
```

in your console. If it says something like "'node' is not recognized as an internal or external command", then Node was not installed properly and you need to go back and try that again. If you see a version number appear, you're set.

## The `node` command

With pretty much any command on the command line, there is built-in help that you can reference just by typing `--help` after the command. Go ahead and try

```
node --help
```

You will see a list appear with some options on how to use the `node` command. There are a few ways to call the command, including running and debugging JavaScript files. For now, let's just stick with the most basic usage of the command:

```
node
```

This will change your prompt to a greater-than sign `>` and allow you to type commands that will be evaluated and printed on the console. This is called the [Read-Eval-Print-Loop](http://nodejs.org/api/repl.html#repl_repl_features), or REPL for short.

## The REPL

Now that you are in the REPL, the fastest way to get out is to hit the keys CTRL+D and hit enter, which will kill the REPL and put you back to the regular command line. Another way is to type 

```
.exit
```

on any line, which will also stop the REPL.

Once you are in the REPL again, try playing around with it a bit. Try math by just typing

```
5 + 6
```

and the REPL will print out `11`. If you want to see everything that is available for you to play with, hit the TAB key. This will give you everything that you can possibly call. It looks something like this:

![](/images/REPL.png)

You can try out any of these objects. For instance, if you'd like to try the `Math` object, just type

```
Math.sqrt(4)
```

to find the square root of 4, 2. I'd also recommend playing with the `process` object, which can tell you a lot about your system and the current running program. For instance

```
process.platform
```

can tell you whether your computer is running Windows or OS X. There are plenty of other methods for process that you can try [here](http://nodejs.org/api/process.html#process_process_platform). Or, if you ever want to just find out on the command line, type `process.` and then hit the TAB key to see a list of all available properties and methods of process.

I am sure you have even more questions now than at the beginning of this blog post, and that's fine. The REPL is a good way for you to play around and figure out some of those answers on your own. If you want to read up on all of those Node.js commands, check out the [documentation](http://nodejs.org/api/). The worst that can happen is that you have to close the command line window and open another one, so don't be afraid to experiment in the REPL!

Have fun, and tweet at me [@thejakepruitt](http://twitter.com/thejakepruitt) if you have any questions!