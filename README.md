# Period5

1. Name attributes of HTTP protocol makes it difficult to use for real time systems:

 -- 1.1 Because the HTTP protocol is only half duplex the server and the user can't communicate simultaneously, so the data can be inacurate, when using the HTTP protocol there's a big overhead opening and closing certain objects like cookies and headers.

 -- 1.2 The http protocol works with request/response sets, as a request is sent to the server it will respond with data via a response. When the transaction is finished the connection is terminated and afterwards the client and the server dont know anything about each other in such. This makes difficult to have a realtime system like a chat server as you would need the server and the client to 'communicate'. So in order to get a real time system to work with the HTTP you can use polling, long-polling or websockets.

2. Explain polling and long-polling strategies, their pros and cons:

To overcome this deficiency, Web app developers can implement a technique called HTTP long polling, where the client polls the server requesting new information.  The server holds the request open until new data is available. Once available, the server responds and sends the new information. When the client receives the new information, it immediately sends another request, and the operation is repeated. This effectively emulates a server push feature. A simple diagram below:

http long polling diagram

For a technical, in depth look at HTTP long polling and implementations for Python, Ruby and JavaScript, check out our article on WebSockets and Long Polling in JavaScript, Ruby and Python.
Considerations for HTTP Long Polling

There are a couple of things to consider when using HTTP long polling to build realtime interactivity in your application, both in terms of developing and operations/scaling.

    As usage grows, how will you orchestrate your realtime backend?
    When mobile devices rapidly switch between WiFi and cellular networks or lose connections, and the IP address changes, does long polling automatically re-establish connections?
    With long polling, can you manage the message queue and catch up missed messages?
    Does long polling provide load balancing or failover support across multiple servers?

When building a realtime application with HTTP long polling for server push, you’ll have to develop your own communication management system. This means that you’ll be responsible for updating, maintaining, and scaling your backend infrastructure.
Backend Infrastructure for Realtime Functionality

With these considerations in mind, that’s where a realtime data stream network like PubNub comes in. PubNub takes care of the backend infrastructure for you, so you don’t have to worry about maintaining and orchestrating your realtime network.

When looking at HTTP long polling with the goal of streaming data, PubNub is a low-latency and low-overhead realtime Web app communication environment, and features the ability to send messages to a single client, client groups and all clients. Upgrading to PubNub is both rapid and easy since PubNub is based on a publish/subscribe model.
Key Benefits of Protocol Agnostic Realtime Messaging

Instead of relying solely on HTTP long polling for realtime messaging, a protocol agnostic approach is beneficial. PubNub automatically chooses the best protocols and frameworks depending on environment, latency, etc. Any server or client code wanting to communicate makes a single API call to publish or subscribe to data channels.

The code is identical between clients and servers, making implementation much simpler than using HTTP long polling. In terms of connection management, the network handles network redundancy, routing topology, loading balancing, failover, and channel access. Additionally, PubNub offers core building blocks for building realtime into your application.

    Presence – Detect when users enter/leave your app and whether machines are online
    Storage & Playback – Store realtime message streams for future retrieval and playback
    Mobile Push Gateway – Manage the complexities of realtime apps on mobile devices, including Push Notifications
    Access Management – Fine grain Publish and Subscribe permissions down to person, device or channel
    Security – Secure all communications with enterprise-grade encryption standards
    Analytics – Leverage visualizations into your realtime data streams
    Data Sync – Sync application state across clients in realtime

  3. What is HTTP streaming, SSE (Server sent events)? :

Streaming is when the browser sends a request, but the server sends and maintains an open response, which is updated and kept open for a defined period of time. The response is updated whenever a message is ready to be sent. The server never requests to finish the response, resulting in the connection being kept open to deliver future messages. A major downside of Streaming is that it includes HTTP headers, which increases data and file size, thus increasing delay.

  4. What is WebSocket protocol, how is it different from HTTP communication, what advantages it has over 
     HTTP?

WebSocket is a protocol providing full-duplex communication channels (allows communication in both directions, and,
unlike half-duplex, allows this to happen simultaneously.) over a single TCP connection.
The WebSocket protocol was standardized by the IETF as RFC 6455 in 2011, and the WebSocket API in Web IDL is being
standardized by the W3C(World wide web).
WebSocket is designed to be implemented in web browsers and web servers, but it can be used by any client or server application..
The WebSocket Protocol is an independent TCP-based protocol. Its only relationship to HTTP is that its handshake is interpreted by
HTTP servers as an Upgrade request.[1] The WebSocket protocol makes more interaction between a browser and a website possible,
facilitating the real-time data transfer from and to the server. This is made possible by providing a standardized way for the server
to send content to the browser without being solicited by the client, and allowing for messages to be passed back and forth while
keeping the connection open. In this way a two-way (bi-directional) ongoing conversation can take place between a browser and the
server. The communications are done over TCP port number 80, which is of benefit for those environments which block non-web Internet
connections using a firewall. Similar two-way browser-server communications have been achieved in non-standardized ways using stopgap
technologies such as Comet.
The WebSocket protocol is currently supported in most major browsers including Google Chrome, Internet Explorer, Firefox, Safari and
Opera. WebSocket also requires web applications on the server to support it.

One difference is that WebSocket provides perform bi-directional, full-duplex communication unlike HTTP. This means that webSockets
allows communication in both directions, and,unlike half-duplex, allows this to happen simultaneously.).
Another difference is that WebSockets require full-duplex connections and new Web Socket servers to handle the protocol.
Furthermore WebSockets lack features such as automatic reconnection, event IDs, and the ability to send arbitrary events. These you
have to implement your self if wanted.

The advantage of the two-way channel that webSockets uses is in the cases where you need near real-time updates in both directions for
things like games and messaging apps. This is a possibility with webSockets where as with pooling it was not.
Furthermore it has an advantage as it has been built from the ground up for bidirectional capabilities with less overhead (headers).
This has a big impact on time if you transfers a great deal of data. Ex. if you needed to exchange a high throughput of messages from
both ends, with almost as much data flow upstream than downstream (e.g Massively Multiplayer Online Game that needs to keep all their
players in sync). WebSocket will remain a better choice.

5. Explain what the WebSocket Protocol brings to the web-world:

WebSocket is a protocol providing full-duplex communication channels over a single TCP connection. The WebSocket protocol was standardized by the IETF as RFC 6455 in 2011, and the WebSocket API in Web IDL is being standardized by the W3C.

WebSocket is designed to be implemented in web browsers and web servers, but it can be used by any client or server application. The WebSocket Protocol is an independent TCP-based protocol. Its only relationship to HTTP is that its handshake is interpreted by HTTP servers as an Upgrade request.[1] The WebSocket protocol makes more interaction between a browser and a website possible, facilitating the real-time data transfer from and to the server. This is made possible by providing a standardized way for the server to send content to the browser without being solicited by the client, and allowing for messages to be passed back and forth while keeping the connection open. In this way a two-way (bi-directional) ongoing conversation can take place between a browser and the server. The communications are done over TCP port number 80, which is of benefit for those environments which block non-web Internet connections using a firewall. Similar two-way browser-server communications have been achieved in non-standardized ways using stopgap technologies such as Comet.

The WebSocket protocol is currently supported in most major browsers including Google Chrome, Internet Explorer, Firefox, Safari and Opera. WebSocket also requires web applications on the server to support it.

6. Explain and demonstrate the process of WebSocket communication -From connecting client to server, through sending messages, to closing connection.

// Create SocketIO instance, connect
var socket = new io.Socket('localhost',{
    port: 8080
});
socket.connect(); 

// Add a connect listener
socket.on('connect',function() {
    console.log('Client has connected to the server!');
});
// Add a connect listener
socket.on('message',function(data) {
    console.log('Received a message from the server!',data);
});
// Add a disconnect listener
socket.on('disconnect',function() {
    console.log('The client has disconnected!');
});

// Sends a message to the server via sockets
function sendMessageToServer(message) {
    socket.send(message);
}
https://camo.githubusercontent.com/6dd1a8c53d58a7a12308041a10f347fc65015aad/68747470733a2f2f7777772e7075626e75622e636f6d2f7374617469632f696d616765732f6765742d737461727465642f776562736f636b6574735f6775696465732e706e67

7. What's the advantage of using libraries like Socket.IO, Sock.JS, WS, over pure WebSocket libraries in the 
backend and standard APIs on frontend? Which problems do they solve?

The advantage of using libraries like Socket.IO, Sock.JS and WS is that it simplifies the usage of WebSockets. Without these librabries are you forced to keep an array of all connections and loop through it to send messages to all clients. The libraries will also provide failovers to other protocols in the event that WebSockets are not supported on the browser or server.
Socket.IO supports autoreconnection, so you don't have to worry about temporary network failures, and finally there are rooms and namespaces support, which makes writing real-time applications much easier and enjoyable.

8. What is Backend as a Service, Database as a Service, why would you consider using Firebase in your 
projects?

Backend as a Service, or BaaS (sometimes referred to as mBaaS) is best described by a tech analyst who refers to it as “turn-on infrastructure” for mobile and web apps. Basically, it’s a cloud computing category that’s comprised of companies that make it easier for developers to setup, use and operate a cloud backend for their mobile, tablet and web apps.

Database as a Service (DBaaS) is a cloud-based approach to the storage and management of structured data. DBaaS delivers database functionality similar to what is found in relational database management systems (RDBMSes) such as SQL Server, MySQL and Oracle. Being cloud-based, on the other hand, DBaaS provides a flexible, scalable, on-demand platform that's oriented toward self-service and easy management,
particularly in terms of provisioning a business' own environment. DBaaS products typically provide enough monitoring capabilities to track performance and usage and to alert users to potential issues. The products can also generate at least some degree of data analytics.

Since Firebase isn’t just any ordinary database, it is a real-time, scalable backend, which provide the tools you need to quickly build rich, collaborative applications that can serve millions of users, only developing client code. Firebase even provides the possibility for authentication. The reasons above describes why i think you should consider using Firebase in your projects.

9. Explain the pros & cons of using a Backend as a Service Provider like Firebase:

ltimately, a Backend as a Service allows you to focus on building the front-end of your app by taking care of all of
 the complex backend plumbing. You care about the user experience, not the backend - that’s not the differentiator in
 your app - so BaaS minimizes the complications of connecting to multiple servers and APIs to set up that backend. Here
 are some more specific pros and cons:
 PROS:
 - Save time: What would be hours or days spent getting your data up and running on cloud infrastructure is just a
   few minutes.
 - Save money: you don’t have to pay a backend developer – who you would need throughout the lifecycle of the app to
   maintain your code – nor do you need to pay to use a cloud provider like Amazon.
 - Richer apps: You’re provided with a core set of mobile features, like geolocation, social, push, data storage, user
   management, analytics, versioning, and blob file storage.
 - More productivity: you should be focusing on what makes your app unique and different - what sets it apart from the
   competition. A backend is not a differentiator. It is an essential component, but your end user doesn't care where or
   how the data gets stored. They care about the user experience. So backend as a service allows you to focus on that,
   the frontend, while they take care of the backend.
 - Data liberation: in addition to the core BaaS features, ie. Kinvey also provides the ability to connect with any
   third-party REST API through a unified interface. This means you only need to learn one backend API, and you can
   switch between data providers with the click of a button. Without a BaaS this would require learning multiple
   APIs - more time, less productivity.
   
 CONS:
 - You don't have complete control of the infrastructure and software stack that your backend is on.  You have only full
   control of your data and the features you use.
 - If the Backend as a Service platform is on a single data center or cloud platform, you may have latency issues if
   your app users are on the other side of the world.
 - The BaaS provider may go out of business.  So make sure you choose the right company that has long-term staying power.
 
