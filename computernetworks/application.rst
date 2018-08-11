Application Layer
=================



Client-Server Architecture
--------------------------

Links :

1. https://www.youtube.com/watch?v=SwLdKeC8scE
2. https://www.youtube.com/watch?v=L5BlpPU_muY

Some things to note :

* Client initiates the connection
* Server is always waiting for clients
* Server responds to Client’s requests
* This is called the Request-Response cycle

###############################################################################

Basics of Network Addressing
----------------------------

IP Address - is a 32 bit number used to uniquely identify a host system(computer).

Port - is a number that uniquely identifies a process on a host.

Together, a given IP and Port uniquely identify a application running on a host in a
network.

We will discuss IP Addresses and Ports in greater detail when we get to Network
Layer and Transport Layer. 

Socket
^^^^^^

The application layer work is done by the code in the application.

The transport layer work is done by services running on the Operating System.

Socket is a software entity that acts as the interface between Application and the Operating System. Therefore, Socket is like a doorway between Application and Operating System - passing packets from Application to OS and vice-versa.

Equivalently, we can call Socket as the interface between Application Layer and Transport Layer.

Relation between Sockets and Ports
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ports and Sockets are very closely related.

Ports are used to uniquely identify a process.

A Socket is the software interface between Application Layer and Transport Layer. An application layer process interacts with the transport layer processes using a socket. During the creation of this socket, a port must be specified, so that the application can be uniquely identified later.

For all intents and purposes, you can consider Ports and Sockets to be equivalent. 

###############################################################################

Transport Layer Protocols available to Applications
---------------------------------------------------

The two most popular Transport Layer protocols available to applications are,

1. TCP - Transmission Control Protocol
2. UDP - User Datagram Protocol

The application developer is free to choose whichever protocol he wants. 

His choice will depend on the differences between the services that TCP and
UDP offer. We will look at this in detail in Transport Layer.

###############################################################################

HTTP
----

Introduction
^^^^^^^^^^^^

HTTP - Hyper Text Transfer Protocol

HTTP began with the Tim Berners-Lee and World Wide Web.

HTTP is stateless

Google, Youtube, Facebook - are all Webpages which are served through HTTP.

Under the Hood
^^^^^^^^^^^^^^

Links :

1. https://www.youtube.com/watch?v=SzSXHv8RKdM
2. https://www.youtube.com/watch?v=po3zYOe00O4
3. https://www.youtube.com/watch?v=fOikWrpPHp0
4. https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol
5. https://medium.com/@hanilim/http-codes-as-valentines-day-comics-8c03c805faa0 - HTTP response codes as Valentine’s Day comics

Key Points
^^^^^^^^^^

1. Works using Client - Server model
2. Thus, works through Request - Response cycles
3. Based on TCP/IP
4. Default server port - TCP Port 80 (Don’t have to memorise)
5. Stateless - Server does not maintain client’s history.
6. Request Methods and Response/Status Codes

	* Request Methods define the action that the client wants to perform. Eg : GET, POST, HEAD etc.
	* Status code is a short 3-digit code which tells the result of the request. Eg : 200 - OK, 404 - Not Found, 403 - Forbidden, 407 - Proxy Authentication Required.

Side Joke
^^^^^^^^^

.. image:: ../_images/httpresponsecodejoke.jpg
   :scale: 65 %
   :align: center

###############################################################################

Cookies
-------

HTTP is stateless. 

The server forgets about the client after each request-response cycle. When the client sends another request, the server does not know about the previous request-response.



Then how does google and facebook “remember” that we are logged in?