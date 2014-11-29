---
layout: post
title: Translation
image: /images/translation.jpg
description: A walk-through on using a Node.js service in a Java application.
---

![](/images/translation.jpg)

With all of the variety that computers have, one of our main challenges is often getting one program to play nicely with the other. For me, the most common difficulty I experience when switching programs is translating document types from Word to Google Docs and to Pages on Mac. I have similar issues when working with presentation types, with elements in PowerPoints and Keynotes being incompatible with each other. At some level, we just want it to work, and have the computer take care of that translation for us.

One problem I had to face recently was handling the communication between a Node.js service and a Java application. I had to find a way to read configuration information from Node.js into a Java server-side application. This kind of translation challenge was very difficult, because while Java and JavaScript have very similar names, certain aspects of the languages make them difficult to translate between each other. In Java, variables need specific types, like integers or strings, while in JavaScript, a variable can have any type.

In the end, the solution I found was to reduce the program down to a level that both Java and JavaScript could understand. This kind of solution exists across almost any translation problem: as long as you can find the one thing in common between the two parties, you can get the message across. When I was in Europe, smiles translated across language and cultural divides. My old violin instructor barely spoke English, so we communicated through music. The easiest way to have the same styling in Microsoft Word and Google Docs is to just use plain text.

In the context of Java and JavaScript I relied on the universal Internet protocol of HTTP and the simple structure of JavaScript Object Notation strings (typically called JSON). I utilized [Seneca.js](http://senecajs.org/) to provide the tools to create a micro-service architecture and the Apache HttpClient [Fluent API](http://hc.apache.org/httpcomponents-client-ga/tutorial/html/fluent.html) to communicate with those micro-services.

## using small words

In Node.js, it is very easy to create a [Microservice Architecture](http://martinfowler.com/articles/microservices.html), which essentially means a lot of small components that each do one thing very well. There are a lot of advantages to microservices, and if you'd like to learn more, there are tons of resources out there, like [the 7 deadly sins of microservices](https://speakerdeck.com/tareqabedrabbo/the-7-deadly-sins-of-microservices) and all of the other talks at [muCon 2014: The Microservice Conference](https://skillsmatter.com/conferences/6312-mucon#skillscasts).

The advantage of using a microservice design when communicating across languages is that you are relying on very well-defined small contracts between the service provider and the service consumer. This means you know what to expect from each side of the language barrier, and can quickly identify problems when communication breaks down.

## establishing a channel

On the Node.js side, I used [Seneca.js](http://senecajs.org/), a microservice toolkit that communicates strictly through small JSON commands. Creating an HTTP API with Seneca is very simple, and allows anything with HTTP client capabilities to interact with it. Just as an example, let's say we set up configuration in Node.js with some property `rate` that was set at `0.23`. We can create a microservice that exposes this information with Seneca.js:

```JavaScript
var seneca = require('seneca')()

seneca.add( {cmd:'config'}, function(args,callback){
  var config = {
    rate: 0.23
  }
  var value = config[args.prop]
  callback(null,{value:value})
})

seneca.listen()
```

This adds the `config` command, that will look up the property that is passed through the `args.prop` argument. We then expose this command as an HTTP endpoint by calling `seneca.listen()` which listens on port `10101` of a local Node.js server for any calls that match that command pattern. Now we can call that command from Java.

## breaking barriers

In Java, my favorite HTTP client library is the [Apache HttpClient Fluent API](http://hc.apache.org/httpcomponents-client-ga/tutorial/html/fluent.html), which has very convenient method chaining for making HTTP requests. After the services above is started and listening on port 10101, we can create a method `act` in Java that will make a call to the service:

```Java
public String act(String json) throws Exception {
	String responseString = Request.Post("http://localhost:10101/act")
          .bodyString(json, ContentType.APPLICATION_JSON)
          .execute().returnContent().asString();

  return responseString;
}
```

This allows us to pass in a JSON-formatted string command to call our Seneca.js microservice:

```Java
SenecaDriver client = new SenecaDriver();
String responseString = client.act("{\"cmd\": \"config\", \"prop\": \"rate\"}");

System.out.println(responseString);
```

This prints out `{"value": 0.23}` to the command line. We have successfully bridged the gap between Java and JavaScript through HTTP and JSON.

All of this code can be found on GitHub in a library called [seneca-java-driver](https://github.com/jrpruit1/seneca-java-driver), which gives the abstraction above for communicating between Java and JavaScript.

How do you approach multilingual programs? Let me know what solutions you've found!