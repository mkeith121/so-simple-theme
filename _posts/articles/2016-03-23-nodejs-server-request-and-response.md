---
layout: post
title: Node.js Server Request and Response
excerpt: "A brief overview of the anatomy of a Node.js server request/ response"
categories: articles
tags: [Node.js, server, request, response]
image:
  feature: nodejs-image.png
  credit: Programmatic Ponderings
  creditlink: https://programmaticponderings.wordpress.com/2015/01/06/calling-third-party-web-apis-from-the-mean-stack/
comments: true
share: true
search_omit: false
---

This article is intended to explore the basic anatomy of a Node.js HTTP handling and server request and response. 

## Creating the Server

The very first step in coming to understand the http server is actually requiring the http module in the file that you plan to contain your server. 

That is accomplished using the following declaration: 

{% highlight html %}
{% raw %}
  <script>
    var http = require('http');
  </script> 
{% endraw %}
{% endhighlight %}

The process, then, for creating the server that is capable of handling requests and sending responses is as simple as writing this expression: 

{% highlight html %}
{% raw %}
  <script>
    var server = http.createServer(function(request, response) {
      response.writeHead(200, {'content-type':'text/plain'});
      response.end("Hello World");
    }).listen(3000);
  </script> 
{% endraw %}
{% endhighlight %}

That's it! That's ultimately all the code you need to set up a server that can runs on your http://localhost: and listens on a specified port.

In the most simplified form, the parameters passed to the function in the createServer call (request, response) contain all the data your server receives with the incoming request and send back with the response. 

The request contains all the information regarding the method of the request ("GET", "POST", "PUT", "OPTION", etc), the url used to access the server, and any data associated with the request. 

The response parameter is the vehicle to transport the servers response. For instance, if the server needs to collect data from a database, the response will receive the data and send it back on the "response vehicle" to be used in the client application. 

And that's about it for the basics!
