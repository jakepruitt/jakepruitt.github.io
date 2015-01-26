---
layout: post
image: /images/struggling.jpeg
description: After a long weekend working away at the Seneca/Hapi/Angular application, I have burnt out too many hours trying to understand authentication. This is a how I feel about the checklist at the moment.

---

![](/images/struggling.jpeg)

Most errors are easy to fix. Explicit call stacks can be read, interpreted, investigated, Googled and troubleshooted rather effortlessly. I remember 90% of my time when I began developing was spent doing this work, and I am amazed that I can now say errors are easy.

The things that are not easy are the errors that are quietly swallowed up in your application. The system mysteriously does not work correctly, and does not give any clues as to why the expected action did not take place. Working with these errors is long and painstaking, and requires hours of inspection; fine-toothed stepping through callback hell that seems endless, senseless, and unhelpful. I am not a great developer, and I have known what it is like to struggle with code. I have learned lessons the hard way before, in AngularJS resource errors, C++ memory leaks, and now in cookie session management between frameworks that were not made to work with each other. I'm struggling right now, and if you think you know how I can get myself out of it, please let me know.

Cut Corners
-----------

If you read [last weeks post](http://javascriptjake.com/2015/01/18/using-express-middleware-with-hapi-js.html), I wrote about building mocked Express request and response objects to interface with Hapi's request and reply objects. The goal was to use those fake objects within an Express middleware function to perform routing on the fly whenever the Hapi server received a request. It seemed to work for a while, but it didn't feel great. I winced when I read over the code, because my implementation of Express's request and response objects were just enough to squeak by the routing problem, but would fall apart if any other unimplemented methods were called.

Soon enough, it became apparent that I would need to rework the implementation. I changed the response mock to be the Hapi `reply` object decorated with just enough Express `response` methods. This implementation seemed a little bit more legitimate, since the response was not just a hollow object, but instead had a whole reply object behind it. Error after error was occurring, with little more than unhelpful server responses to help me. I repeatedly dove into the callback hell and emerged with the specific method that the code was expecting, implemented what was enough to get by, and provided the server-side equivalent of duct-tape to the fundamental problem that I was facing. I was trying to make two incompatible frameworks work together by using a Trojan horse that looked more like a rabbit.

Current State
-------------

So I feel like my attempts have almost been knocked back to square one. I need to figure out where a missing response header has disappeared within thousands of lines of undocumented, uncommented callback soup. These are the hardest parts for me right now:

1. **Lack of experience:** the biggest struggle for me lies in the solitude of remote work. Remote work is wonderful for experienced developers that already grasp concepts and have made enough mistakes before. I am still in the process of making my first mistakes, and while I spin my wheels trying to overcome the hurdles that experienced developers would leap in a single bound, I struggle to sink or swim in a silent empty ocean of other peoples' code.
2. **Lack of direction:** being on the other side of the world from my mentor makes direction very challenging. Simple questions can be asked and answered easily, but sometimes there are larger, more difficult questions that I am not experienced enough to ask correctly. I can't find the right words to asynchronously voice my frustrations or current situations as easily as just leaning across a desk and asking someone to look at the code with me. I find myself making mistakes that could easily be avoided and working very hard to go down dead-end paths. These problems are simple ideas like "Why do you want to use Hapi, exactly?" and "Do you know if this code will work in the long run?" They would take five seconds in person, but are very difficult over written communication.
3. **Lack of documentation:** one of my biggest problems is the lack of documentation of Seneca plugins that I am trying to use, which typically are thousands of lines of poorly commented code. Minor differences between versions are not recorded, and tests are often not updated to keep up. Using test code may work in specific circumstances, but requires extensive introspection when trying to make it work with Hapi, which it was not made to do. The mental model that the writer had when writing the code is completely missing for me, and without this, I feel like I am trying to use a smartphone without ever having seen one before.

I think my next move will be to rework my hapi/seneca interface to fully implement as many Express request/response methods as possible, and completely fool the middleware to think that it is working with Express, and there will be no more swallowed errors like broken headers and cookie functionality. This will take quite a bit of research into the APIs of both Hapi and Express, but hopefully will produce a robust Hapi-to-Express interface that could be reused elsewhere. Unfortunately, this extra work will push back the deadline for the checklist application. The semester is gearing up, and I am afraid that my future will have less and less free time to devote to this project. If you have any thoughts or encouragement, please let me know!
