## HTTP/2
The HTTP 1.1 specification has been around for many years and was developed in a timer where we just could imagine the web applications we would build to day. The new demands of todays web applications push the limit for these old specifications and the industry realize that an upgrade is necessary.

The main problem has always been the performance. Of course we have seen faster and faster web pages when we were getting faster and faster internet connection but thats not enough for demanding application. If you study web traffic you can see that the big performance thief is latency, meaning the time it takes for clients and servers to handle connections and sending HTTP traffic throw these.

The real problem is that HTTP that supports a request/response flow is good for just getting a single document and maybe a few static resources like images and CSS-files. Just do a request let the server response and then close the connection to free up memory to handle new requests.

But todays  web application probably do more then 100 request for just loading one page with all its images, script-files, stylesheets and dynamic content. Since HTTP is using TCP as a transport protocol and TCP is built for longer connections (it have what we call a slow start for making a connection) web traffic must open up more connections to the server to get all the stuff. A browser has the ability to have about 8 simultaneous connections which means that we will get unnecessary latency in a request for a web application. This is a problem that HTTP/2 is suppose to fix.

### How it started
Google started to develop a web traffic protocol which they called SPDY (pronounced speedy). This work has been the base for HTTP/2 protocol that is developed by the IETF (Internet Engineering Task Force) who are now leading this work which is supported by partners as Google, Microsoft, Apple which means it will have/have support in all major browsers. The specification was published as a proposed standard in may 2015 in the [rfc 7540-document](https://tools.ietf.org/html/rfc7540)

### Whats new?
There are several changes in this protocol that addresses the performance problem. Here is a short list of the key features:

* HTTP/2 uses what we call multiplexing that allow server and client to have just one TCP-connection and send all its data throw that. In HTTP 1.1 there is a thing call [HTTP pipelining](https://en.wikipedia.org/wiki/HTTP_pipelining) which allow a client to send multiple HTTP requests are sent on a single TCP connection without waiting for the corresponding responses. This is called [Head-of-line blocking](https://en.wikipedia.org/wiki/Head-of-line_blocking). In cases where two requests sends to server, the first is large and the second small. In HTTP 1.x we must wait for the first to be processed and responded before it can be respond the second smaller message. This is solved in HTTP/2.
* The HTTP headers are used in the same way but there is a smarter way that avoids sending redundant information.
* The server can push resources it realize the client will be needed. For example a index.html is requested, the server can then push the linked css- or script-file without the client needed to first get the index.html, parse the HTML and then requesting the files.
* Nothing will be changed for the developer, all HTTP Status, methods and stuff we know will be the same. But one thing is worth mention. In HTTP/2 its OK to let the client application do lots of request since we can send all of them in one TCP connection.

## Further resources
Above is just a small introduction to get a deeper understanding of HTTP/2 and what performance benefits we will have from it you should look at [this presentation](https://www.youtube.com/watch?v=yURLTwZ3ehk) by Ilya Grigorik, one of the leading person of the HTTP/2 development.

You can also read about this things in his book [High Performance Browser Networking](http://chimera.labs.oreilly.com/books/1230000000545/index.html)
