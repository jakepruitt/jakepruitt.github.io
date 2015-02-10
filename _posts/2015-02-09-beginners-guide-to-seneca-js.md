---
layout: post
title: Beginner's Guide to Seneca.js
image: /images/beginners-guide-to-seneca-js.jpg
description: This guide introduces Seneca.js, explains the basic ideas of Seneca, and provides best practices for using Seneca in your own projects.

---

![](/images/beginners-guide-to-seneca-js.jpg)

When I started looking into [Seneca.js](http://senecajs.org/), I did not fully understand why I would want to use it in my project. I was a true beginner at Node.js applications, and did not have any idea what words like "micro-services" or "business-logic" really meant.

After a few weeks of misguided attempts, refactoring, and source code inspecting, I slowly became comfortable working with Seneca and built out a [checklist application](https://github.com/jrpruit1/checklist) that uses Seneca to organize the back-end API. I discovered quite a bit about application architecture, data-manipulation, and RESTful services along the way, and also learned for myself exactly what Seneca provides, without any abstract vocabulary. My experience of learning the toolkit from the ground up helped me really understand what is missing in the current literature, and where my pain points were as a beginner learning Seneca.

This guide is a product of those pain points; the disambiguated guide for absolute beginners I wish I had two months ago.

What Seneca.js is not
---------------------

For me, it can sometimes be useful to understand what something is not before describing what it is. I love comparisons, and I am quick to make hasty generalizations that can end up hurting me in the long run. To avoid that, here is a list of what Seneca is not:

1. **Seneca is not an opinionated framework-** There is no "This should go here and that should go there" with Seneca. Want to put all of your application in one action? You can. Want to make every action only 5 lines of code? You can do that too. Seneca is incredibly robust, and will work with just about any architecture decisions you make.
2. **Seneca is not a beginner-friendly application generator-** There is no "Just add water" magic that beginners can lean on to instantly build applications. When I began using Seneca, I had never worked with server-side JavaScript applications before. I was completely lost, and since Seneca is unopinionated, I continued to stay lost. Only after I gained a good grasp on server-side architecture was I able to effectively use Seneca. If you know what you are doing, Seneca is incredibly helpful. If you're not sure what you are doing, Seneca will not solve your problems for you. It is only as good as the programmer using it.
3. **Seneca is not a small utility library-** Seneca is not like a lodash zero-dependency read-through-in-one-afternoon module that you can include and sprinkle throughout your application. Seneca is robust, quite large, and pretty involved under the hood. Seneca weighs in between Hapi and Express in terms of size (comparing gzipped releases and directory sizes within node_modules). This makes sense when you consider that Seneca must solve very tough problems around pattern matching, action execution order and process communication.

So what is Seneca?
------------------

Now that you have read through those three points, you are probably quite confused about what Seneca actually *is*. After describing this framework many times and using lots of different terms and phrases, I have found this definition of Seneca to be the most useful:

> Seneca is a tool that separates an application into small actions.

This definition is an oversimplification of everything that Seneca provides, but it is the core of what Seneca accomplishes. The only ambiguous term in that definition is the word "action", which is the irreducible element of a Seneca application, and the most important abstraction provided by toolkit.

Actions Explained
-----------------

An **action** is a function that is identified by a JSON object. Actions lie at the core of Seneca, and in order to use Seneca, a developer must be able to think in terms of small functions that can be called from anywhere by their JSON identifiers. Actions are created using the `seneca.add` method:

```JavaScript
seneca.add({role:'inventory', cmd:'find_item'}, function(args, done) {
  var itemId = args.id;

  // find item using any means necessary
  var item = byAnyMeansNecessary(itemId);

  done(null, item);
});
```

Actions can have any granularity and any JSON pattern. You can have actions from `{application:'myApp', accomplish:'everything'}` to `{ module:'addition', perform:'onePlusOne', because:'reasons'}`. As a personal style, and a convention found throughout Seneca plugins, I tend to keep my actions in the format `{role:'namespace', cmd:'action'}`, where "namespace" is the logical grouping of a few actions and "action" is the name of the specific action that I want to define.

Calling actions can be done using the `seneca.act` method:

```JavaScript
seneca.act({role:'inventory', cmd:'find_item', id:'a3e42'}, function(err, item) {
  if (err) return err;

  console.log(item);
  // Perform other actions with item
});
```

To put it in perspective, I tend to define related actions all in the same file with the same role (for instance file `todo-list.js` would have all tasks with role `todo_list`). As a rule of thumb, I try not to let this file get larger than 150 lines or so, and try to keep each action definition small enough to read without scrolling. Other people may have different preferences, but that size feels comfortable to me.

Why Actions?
------------

So now that you have a basic idea of the atomic element of Seneca, you are probably wondering about the purpose of breaking a system up into action definitions and action calls. The purpose here is to create **enforceable boundaries** between the components of your application, which forces you to think in a more modular pattern and avoid the desire to throw everything in one main file. As we will see soon, once an application has been divided into actions, Seneca provides an abundance of tools to expose actions as HTTP microservices or url addressable web servers. 

Organizing actions into files
-----------------------------

I mentioned earlier how I keep all related actions in a single file, but did not describe how I attached those actions to the seneca instance in another file. Seneca comes with the `seneca.use` method that finds a matching file or module and incorporates it into the seneca instance. For example, if I had a few actions that all had to do with inventory, I would create an `inventory.js` file and define all of the actions there:

```JavaScript
/* inventory.js */
module.exports = function(options) {
  var seneca = this;

  seneca.add({role:'inventory', cmd:'find_item', find_item);
  seneca.add({role:'inventory', cmd:'create_item', create_item);
  //... other action definitions

  function find_item(args, done) {
    var itemId = args.id;
    // ... perform find
    done(null, item);
  }

  function create_item(args, done) {
    var itemName = args.name;
    // ... perform item creation
    done(null, item);
  }
}
```

And I would use the `inventory.js` file in my `server.js` file:

```JavaScript
/* server.js */

var seneca = require('seneca')();

seneca.use('./inventory.js');

seneca.act({role:'inventory', cmd:'create_item', name:'apple'}, function(err, item) {
  console.log(item);
}
//...
```

Notice that we have a reference to the seneca instance in `inventory.js` through the `this` variable. After we add actions to the instance, we can call those actions in the server.js file. The general format in `inventory.js` of calling `seneca.add` at the top and defining methods after is not mandatory, it's simply a convention followed by a few other plugins.

Hundreds of existing plugins can be leveraged to bring pre-built actions into your application, from Express server integration to authentication and database access. The ecosystem is quite extensive and can make application writing much faster once you understand how to call the actions.

The Next Level: Multiple Node Processes
-----------------------------------------

In the above example, the application can be started by running `node server.js` and everything will occur on that process. However, what if you wanted multiple processes running, one that simply handled the inventory actions and another process that consumed them. Inter-process communication can be tricky for Node applications, but Seneca allows you to make this change with only two changes in your code. We will keep the `inventory.js` file the same as before, exposing the actions as a Seneca plugin. However, we will create two main files, one called `inventory-service.js` that will run the service on port 10101 using `seneca.listen` and another file `inventory-client.js` that will use `seneca.client` to access the service and use its actions.

```JavaScript
/* inventory-service.js */

var seneca = require('seneca')();

seneca.use('./inventory.js');

seneca.listen();
```

We can now run `node inventory-service.js` in one tab and it will be listening on port 10101. In `inventory-client.js` we can write:

```JavaScript
/* inventory-client.js */

var seneca = require('seneca')();

seneca.client();

seneca.act({role:'inventory', cmd:'create_item', name:'apple'}, function(err, item) {
  console.log(item);
}
// ...
```

Running `node inventory-client.js` will now perform the same thing that `node server.js` performed in the previous example, only now we have begun scaling our application horizontally across multiple processes. This is the true benefit of using Seneca: since we have abstracted our application into small actions, those actions can be declared in different files or even different processes. Using the plugins available for web integration, actions can even be run on separate hosts.

Further Reading
---------------

Now that you understand a small part of what Seneca provides, you can begin making your application more modular and scalable. Here are some further readings to find out more about Seneca and microservices in general:

* [Build a Search Engine using Microservices](http://blog.skillsmatter.com/2014/09/10/build-a-search-engine-for-node-js-modules-using-microservices-part-1/)
* [Falling in Love with Technical debt](http://www.slideshare.net/rjrodger/richard-rodger-technical-debt-web-summit-2013) (talk)
* [Microservices](http://martinfowler.com/articles/microservices.html) (long-form explanation of microservices)
* [Well app](https://github.com/nearform/well) (example application)
