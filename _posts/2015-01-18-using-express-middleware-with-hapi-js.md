---
layout: post
image: /images/using-express-middleware-with-hapi-js.jpg
title: Using Express Middleware with Hapi.js
description: I've just emerged from a personal odyssey through the source code of an Express middleware, navigating through services, routers, dispatchers, handlers and responders to understand how to use this middleware in a Hapi.js server. This is what I learned.

---

![](/images/using-express-middleware-with-hapi-js.jpg)

My roommate recently told me how he used to believe in magic. He thought driving involved magic whenever he watched his parents operating a fast-moving wheeled machine through unseen foot movements and experienced wheel turnings. But once he was older, he knew just how the pedals applied pressure, how the engine used gasoline to accelerate the wheels, how friction was used to stop the car, and realized that there was no magic involved at all. In fact, nothing involves magic when examined closely, and all it takes is curiosity and persistence to overcome any fears we have associated with not knowing how something works.

I recently completed a personal odyssey through the source code of [seneca-web](https://github.com/rjrodger/seneca-web), a seneca plugin that allows users to map routes to seneca actions. The plugin exports an Express middleware function for responding to route requests with actions registered with seneca's `role:web` action. For the longest time, I assumed that express middleware was just magic, and all that could you could possibly do is trust the middleware or write your own middleware from scratch.

It took hours of careful reading and inspection to finally understand how to turn the express middleware into a usable Hapi.js plugin. At best, it felt like a detective novel with winding mysteries that were revealed by well-placed clues and stunning reveals. At worst, it felt like reading a novel in Japanese with only a Japanese dictionary to help.

Eventually I worked out a good system to removing the mysticism and magic of complicated library source code, and create a solution that cut elegantly through the winding closures and callbacks of the middleware.

Initial Attempts
----------------

My first task when dealing with seneca-web was not understanding how it worked, but just understanding what it did. Without very thorough documentation, I slowly worked through the API, which involved a handful of seneca actions and one export function in the form of an Express middleware. After hours of reading, testing, and debugging, I began to understand the necessary parameters for every action and the format of the outputs of every function.

I knew that every call to `role:web, use:{...}` internally added a route to a route table that mapped to a "service". At the time, I was not sure at all what this "service" was, and figured that it involved some sort of magic. In my mind, I figured I could just create a route handler for Hapi.js that would use seneca-web to find the corresponding "service", call the "service" with the Hapi request and reply objects, and then call `next()` and be finished. It sounded easy enough, and I could escape without knowing the underpinnings of what was in a "service" or how the exported middleware function worked.

Walking in Circles
------------------

That solution did not work, and I had no idea why. I had called the right service, but the internal workings of the service did not want a Hapi request and reply object, they wanted some other mysterious object that I could not figure out. After a few frustrated attempts at changing the parameters, I thought that I could write my own seneca plugin, without the need for seneca-web, and write it better. I figured I could remove any complications and write something that just worked, clean and simple.

It wasn't long before I realized just how wrong I was. I think our initial reaction of "Well that's crazy, they're overthinking it. I could build it much simpler" is often an gross underestimation of how complicated the problem is and an arrogant overestimation of our own abilities. I soon hit a number of walls that lead me back to reading the way the seneca-web "services" really worked. I treaded and retreaded the same water in the source. I even printed the source code to try to map the way services were created and called.

Breaking through
----------------

I'm not sure why I did not think of using [node-inspector](https://github.com/node-inspector/node-inspector) sooner, but once I remembered the debugger, the problem quickly unfolded. I stepped through the creation process of a service, which revealed to me the nuanced difference of returning functions, calling callbacks, passing callbacks, and defining functions that I did not know before. I was slowly discovering the mental model of the code's author, and retracing his steps like a carefully placed scavenger hunt. The debugger revealed to me the state of every object at every step of the process, and the supreme significance that closures have in server-side JavaScript. I learned how express routers use regular expressions and the methods called on response objects when the conclusion was actually reached.

When I realized the complexity involved in routing, dispatching and responding to requests, I realized that I should lean on the seneca-web work as much as possible to provide the same functionality in Hapi.js. I found that the only methods used on the response object were `res.writeHead` and `res.end`. My solution created a facade of a response that mapped the response methods to corresponding methods of the Hapi.js reply object. It felt a bit hacky, and certainly does not provide for every contingency, but I realized that I could accomplish much more by standing on the shoulders of the seneca-web logic and conforming to that model than making that model conform to me. The current result of hapi-seneca is as follows:

```JavaScript
var hapiSeneca = {
  register: function (server, options, next) {
    var seneca = options.seneca;

    server.ext('onRequest', function(request, reply) {
      var req = request.raw.req;
      var status = 200;
      var headers = {};
      var res = {
        writeHead: function(resStatus, resHeaders) {·
          status = resStatus;
          headers = resHeaders;
        },
        end: function(objstr) {·
          var res = reply(objstr);·
          res.code(status);
          for (header in headers) {
            res.header(header, headers[header]);
          }
        }
      };
      seneca.export('web')(req, res, function(err) {
        if (err) { return reply(err); }
        reply.continue();
      });
    });

    next();
  }
};
```

I learned quite a bit from working on this project. Hopefully, this abstraction will work in most cases, and if not, I will rework it as needed. Maybe this model would even work for other middleware/Hapi compatibility things in the future, in which case I could abstract this to a hapi-middleware module. Please let me know what you think! I know I haven't implemented all of interface methods of the ServerResponse yet, but hopefully this will get me through.
