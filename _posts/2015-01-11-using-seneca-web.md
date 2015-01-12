---
layout: post
image: /images/using-seneca-web.jpg
title: Using seneca-web
description: After spending a day intimately getting to know the seneca-web plugin for the Seneca JavaScript framework, I have learned quite a bit about how seneca can be used to define a web api.

---

![](/images/using-seneca-web.jpg)

After spending a day traversing the inner-workings of Seneca's `seneca-web` plugin, I have learned quite a bit about using Seneca to create a web API. [Seneca](http://senecajs.org/) is a JavaScript toolkit for creating and using microservices, which allows developers to break up their applications into small bite-sized homogeneous pieces, each of which do one thing really well. The name Seneca comes from the Roman philosopher Seneca the Younger, who was a member of the stoic school of philosophy, which emphasized a simple, unperturbed, practical life, which happens to relate well to the architecture of microservices in the software development world. 

Seneca as I know it
-------------------

With little documentation and a very large source, it has not been easy for me to wrap my mind around the way a developer should use Seneca. After a few months of work, hours of source code reading, and quite a few plugin documentations, the following checklist describes my mental model of Seneca:

1. Seneca, at its heart, is an EventEmitter that uses JavaScript objects instead of strings to register and call events
2. `seneca.add()` allows a developer to create a pattern for a specific action
3. `seneca.act()` allows a developer to perform an action
4. Seneca employs a plugin system to easily break apart application code. By integrating a plugin, for instance `seneca.use('web')`, a variety of pre-defined commands become available to use.

That is the very basic essence of Seneca, which has quite a bit of complex logic internally for executing the actions in order, and provides many other external functions like `seneca.listen()`, `seneca.export()`, `seneca.client()` and so on.

**PRO TIP:** one of my biggest problems when starting with seneca was gaining insight to the state of the seneca object. After playing around on the REPL with seneca, I discovered one of the most important functions of seneca:

```JavaScript
seneca.list();
```
This method returns an array with all of the possible actions that are currently registered on the seneca instance. This was a great way for me to debug my application, especially when trying to figure out seneca-web.

Seneca over HTTP
----------------

It took quite some time for me to finally grok the way seneca created a web API. There are lots of ways to expose the seneca actions to HTTP methods, including the `seneca.listen()` method, which listens for POST requests on `http://localhost:10101/act` and responds to the actions specified in the JSON request.

Another method for setting up an HTTP interface for seneca is to register commands with the seneca-web `use` command. This creates routes that map to the services, and these routes can be added to an express or connect app by using the `seneca.export('web')` method. The following example illustrates this method:

```JavaScript
var seneca = require('seneca')()

seneca.add('role:foo,cmd:bar',function(args,done){
  done(null,{bar:args.zoo+'b'})
})

seneca.act('role:web',{use:{
  prefix:'/foo',
  pin:{role:'foo',cmd:'*'},
  map:{
    bar: {GET:true}
  }
}})


var connect = require('connect')
var app = connect()
app.use( connect.query() )
app.use( seneca.export('web') )
app.listen(3000)

// run: node test/example.js --seneca.log=type:act
// try http://localhost:3000/foo/bar?zoo=a
// returns {"bar":"ab"}
```

The nice part about this method is that the API can simply be defined on the basis of the routes. The only difficulty is that the web server must be an express server, and cannot be a Hapi server or Director server.

**PRO TIP:** One of the handiest commands available for seneca-web is the `'role:web, cmd:routes'` command. This passes an array of all of the routes to a callback, which then can be logged and inspected. For instance:

```JavaScript
seneca.act('role:web, cmd:routes', function(err, routes) {
  console.log(routes);
});
```

Making Seneca Hapi
------------------

Right now, I am working on a Hapi plugin that will create the routes stored in seneca-web and map those routes to the appropriate commands. So far, I have really enjoyed working with Hapi, and find its API very robust and solid. I now have a much better idea of how the `seneca-web` component of the system works, and will use that to marry the super-powered web framework of Hapi with the microservice mindset, and hopefully some best practices will surface.

If you are interested in following the Hapi/Seneca progress, check out the [Checklist application](https://github.com/jrpruit1/checklist) that I am building using **B**ootstrap, **A**ngular, **S**eneca, and **H**api (or **BASH**). Most of the application is smoke tests at this point, but the components have been chosen carefully to be simple and robust.

Later this week, I will have a post about the decisions I have made setting up a **BASH** application, and possibly create a Yeoman generator that can scaffold out a similar application from the command line. My goal is to constantly simplify the application to its core components, and once I have built an intuitive way for Seneca and Hapi to communicate, I will have most of what I need.
