---
layout: post
title: Introspection
image: /images/introspection.jpg
description: In this article, we examine how to debug a node application using the built-in node debugger.
---

![](/images/introspection.jpg)

Programming is not an easy job. As a developer, you are tasked with taking ideas and [translating them into a language a machine understands](/2014/11/04/fundamentals.html). And it can be very difficult. You can only know so much of what your code is doing, and a lot of it you are faking or relying on an answer you found online that seems to work.

And it's okay that you don't know it all. [There is no such thing as a genius programmer](https://www.youtube.com/watch?v=0SARbwvhupQ). Everyone has struggled through programming, which should make you feel better about that weird error you keep getting that has taken you hours to fix. Being an experienced programmer does not mean that you know everything that a computer does and can rattle off Node.js documentation in your sleep. Some of the best programmers I know still turn to Google whenever they need to work with regular expressions. The value in being an experienced web developer is that you have made more mistakes than a new developer. And if you can learn from those mistakes, the next time you see them, you will know how you solved them before.

This article is a workshop that helps you familiarize yourself with the `node debug` tool, and starts teaching you the invaluable skill of finding bugs within your code and fixing them. I cannot teach you how to solve every bug you will ever see, I can only show you the tools to catch them. Good old "give a man a net" idea.

*Note: If you are not familiar with Node.js or programming at all, I suggest you go back and read my earlier blog post on [good learning resources](/2014/11/02/curriculum.html), or check out one of the great tutorials on [Node School](http://nodeschool.io/), especially the `learnyounode` one.*

## The problem

One common use case for Node.js is to set up a server that works as a RESTful API, or in other words, responds to incoming requests with data based on the parameters you pass it in the request. Think of this as a food truck that will take your order and serve you hot dogs, only the food truck is a web address (like "https://connect.foodtruck.net/api.js"), your order is the value passed into the end of the address (like "?mustard=true"), and the hot dog is the JSON data object that is returned (like {"id":122, "type":"hotdog"}). Pay attention sometime to the URLs of websites and you can see these parameters in action.

To keep it simple, let's say you want to create an API that takes the query parameter "num", multiplies "num" by 2, and returns a JSON object with field "num2x". In real life, we would probably use a module like [Express](http://expressjs.com/) to do this, but for the sake of the argument, let's say we had to do it just with the basic Node.js core modules.

## The boilerplate

We will start with the most basic http server possible:

```JavaScript
// in server.js

var http = require('http');

http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World\n');
}).listen(1337, "127.0.0.1");
```

This code should look pretty familiar to you, since it is the code on the [Node.js homepage](http://nodejs.org/). When we run `node server.js` on the command line, we get no output (hopefully) and when we navigate to `http://127.0.0.1:1337` in our browser, we see the text "Hello World" at the top of the page.

We can run `node debug server.js` there is nothing interesting going on. We can step through the file by typing `next` repeatedly into the debug prompt, and see that the file successfully executes to the finish.

## Ear to the pavement

The first piece of advice I can give you is to utilize `console.log()` as a tool to protect against future problems. To do this in our server script, add the following console logs:

```JavaScript
// in server.js

var http = require('http');

http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  console.log("Request recieved at: ", (new Date()).toLocaleString());
  res.end('Hello World\n');
}).listen(1337, "127.0.0.1");

console.log("Server listening at 127.0.0.1:1337");
```

And then we run `node server.js` and request the url in our browsers and see the following output to our console:

```
Server listening at 127.0.0.1:1337
Request recieved at:  Thu Nov 06 2014 22:02:22 GMT-0700 (US Mountain Standard Time)
Request recieved at:  Thu Nov 06 2014 22:02:22 GMT-0700 (US Mountain Standard Time)
```

Why is it saying we requested it twice? Maybe we need a bit more visibility, so let's add another `console.log()` to tell us what the url is that is being requested:

```JavaScript
...
console.log("Request recieved at: ", (new Date()).toLocaleString());
console.log("URL Requested: ", req.url);
...
```

Now the output should look like this:
```
Server listening at 127.0.0.1:1337
Request recieved at:  Thu Nov 06 2014 22:09:32 GMT-0700 (US Mountain Standard Time)
URL Requested:  /
Request recieved at:  Thu Nov 06 2014 22:09:33 GMT-0700 (US Mountain Standard Time)
URL Requested:  /favicon.ico
```

Awesome, so it looks like our browser was just requesting the favicon for the site that goes at the top of the browser tab. We now have pretty good visibility into our server's actions.

## Controlling the request

Before we go on, we are going to need to write a client script that acts like the browser and requests information to our server. This will allow us to debug easier, and not have the issue of requesting the favicon every time. In another JavaScript file, add the following code:

```JavaScript
// client.js
var http = require('http');

http.get("http://127.0.0.1:1337/", function(response) {
	console.log("Connection made");
	response.pipe(process.stdout);
});
```

This will do the exact same thing the the browser was doing before, only now we have more control over the request since we run it from the command line and can output the response right there.

Now if we run `node server.js` in one command window and leave it running, and then run `node client.js` in another window, we should see the server output that it was requested, and the client output:

```
Connection made
Hello World
```

Now we can start doing some interesting things. 

## Freeze frame

Since our `client.js` file has control of the request, we can add `debugger` breaks to examine the internals of the system at that point. In `client.js`, add the `debugger;` statement above the `console.log` statement:

```JavaScript
// client.js
...
http.get("http://127.0.0.1:1337/", function(response) {
	debugger;
	console.log("Connection made");
...
```

When we run the `client.js` file with `node debug client.js` we get the following output:

```
< debugger listening on port 5858
connecting... ok
break in C:\Users\Jake\Documents\JakeWebsite\debug-example\client.js:1
  1 var http = require('http');
  2
  3 http.get("http://127.0.0.1:1337/", function(response) {
debug> cont
break in C:\Users\Jake\Documents\JakeWebsite\debug-example\client.js:4
  2
  3 http.get("http://127.0.0.1:1337/", function(response) {
  4     debugger;
  5     console.log("Connection made");
  6     response.pipe(process.stdout);
debug> cont
< Connection made
< Hello World
program terminated
```

By adding the `debugger` statement, we can freeze the program right before the console.log statement. This allows us to do things like call `repl` and examine the response object properties in the middle of the callback! I personally think that is very powerful, and gives us a lot more control over the execution of the file.

Now remove that debugger statement in `client.js` and instead add it in `server.js`, right before the `res.end` call:

```JavaScript
res.writeHead(200, {'Content-Type': 'text/plain'});
debugger;
res.end('Hello World\n');
```

Now restart your server with `node debug server.js`, and type `cont` to make it run through execution. Then, when you run `node client.js` the server window should pause at the `debugger` call and nothing should show up on the client yet. Now you can access the response and request objects from the server side!

## Using the `repl` to debug your code

While you are paused at the `debugger` statement, type `repl` into the command line and the repl will appear. You can now examine the request object by typing `req` into the command line.

More importantly, you can test out different responses on the fly from the repl. For instance, try typing

```
res.write("Hey there");
```

If you have the `node client.js` window still open, you should see `Hey there` appear on the screen. Pretty cool!

## Parsing the url

To make things a little easier, let's change something in the `client.js` really quickly:

```JavaScript
...
http.get("http://127.0.0.1:1337/?num=" + process.argv[2], function(response) {
...
```

This allows us to pass the number we want to test to the command line call. Now we can type `node client.js 2` and the request will have the parameter num=2.

Now when we are paused at the `debugger` statement on the server, we can examine the url parameter by entering the REPL and typing:

```
> req.url
'/?num=3'
> req.url.slice(2)
'num=3'
> req.url.slice(2).split('=')
[ 'num', '3' ]
> req.url.slice(2).split('=')[1]
'3'
```

We figured out how to get the 3 from the URL parameter just with string methods. Now in `server.js` we can add:

```JavaScript
res.writeHead(200, {'Content-Type': 'text/plain'});
var num = req.url.slice(2).split('=')[1];
var answer = JSON.stringify({num2x:num*2});
res.end(answer);
console.log("Request recieved at: ", (new Date()).toLocaleString());
```

And now our `node client.js 3` call prints `{"num2x":6}` to the console! We did it!

## Why didn't you just write that last part?

It was a long process to get here, and I know parts of this were redundant, because I am still learning a lot of this. I did not write this post about creating an API that can multiply numbers by two and send JSON. That would have taken 2 minutes.

Instead, I wrote a long article that showed you the process of how you can tackle problems while weilding the tool of `node debug`. I wish someone had done this for me when I started. 

Was this valuable to you? Was it overkill to describe the entire process, or did it help you understand node debug? Personally, I learned a lot about this workflow by writing it all out, and will be much more comfortable using `node debug` in the future. If you want to learn about more debugging tools, check out [node inspector](https://www.npmjs.org/package/node-inspector) and [this great article](http://www.100percentjs.com/best-way-debug-node-js/) compares different tools.

Until tomorrow!