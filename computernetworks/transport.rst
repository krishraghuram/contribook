Transport Layer
===============
    
    *We will cover Transport Layer in more
    detail than any other layer.*

Interface between Application Layer and Transport Layer
-------------------------------------------------------

The transport layer provides logical communication between applications
(same as processes in this context).

In other words, to the application processes 
(both client and server side) it is as if they are 
communicating to each other directly,
as if they were running on the same system.

Transport layer "abstracts away" the lower level details from the
application.

**How is this done?**

An application on one machine, wants to connect to another
application on a different machine. Thus, the application requests
transport layer service for aid. The transport layer service is usually
part of the OS.

The transport layer service, needs to know which applications need to
communicate, and what machines they are running on. In other words,
it needs,

* Destination IP
* Destination Port
* Source Port
* Source IP

Usually, the transport layer service can safely assign a unused
source port. It can also get source ip from the network layer service
or operating system. Thus, the Destination IP and Port are the crucial
details that the application must provide.

Recall sockets - The interface between application and transport
layer - During creation of a socket, the application has to specify
these details.

.. admonition:: Example

    As an example, consider a web-browser.
    It is an application, and uses HTTP, HTTPS, DNS etc.
    for allowing user to browse the internet.

    When you want to access google or facebook,
    the web-browser needs to specify the four details. 

    The browser does not worry about the source IP and port -
    the transport layer can get the ip from network layer,
    and it can also assign an unused port.

    But the browser needs to give the destination IP and
    port. Who sets this???

    We do. When we type in the url bar **http://www.google.com**,

    * the browser takes default port 80
      (Recall that http’s default port is 80).
    * the browser makes a dns request to find the IP of www.google.com
      (Recall that DNS is used for name -> IP translation)

    The browser creates a socket using the above details,
    and is able to get the website.

########################################################################

Interface between Transport Layer and Network Layer
---------------------------------------------------

How does Transport Layer interact with Network Layer? 

Transport Layer provides **logical communication between processes**.
Network Layer provides **logical communication between hosts**.

For this, Transport Layer must provide the Network Layer with 
Source IP and Destination IP. Recall that the Application Layer
passed these details to the Transport Layer.
Transport Layer just needs to pass them down onto the Network Layer. 

Read more from Kurose and Ross Section 3.1.1 

The Network Layer protocol that is used by both TCP and UDP, is IP -
Internet Protocol. IP’s service model is called best-effort delivery.
This means that IP makes best-effort to deliver packets properly,
but it makes no guarantees.

As we will see, TCP and UDP have the tasks of, 

* Providing a process-process communication
  using a host-host communication.
* Additionally, choose to provide services such as,

    * Error Detection and Correction
    * Reliable Data Transfer
    * In-Order Arrival
    * Flow and Congestion Control

We will see how transport layer solves 
these problems in the next sections.

########################################################################

Why did we spend so much time on interfaces?
--------------------------------------------

It is counter intuitive that we discuss so much about "interfaces",
which are, strictly speaking, not part of transport layer itself.

But interfaces are important. Interfaces tell us what is expected from
things that are above us, and what is provided by things that are below
us. Thus, it tells us exactly what "gap" we are to fill.

What it doesn't tell us, is how we fill that gap. That comes below.

########################################################################

Multiplexing and Demultiplexing
-------------------------------

We need to provide process-process communication from host-host
communication.

Multiplexing is a method of sharing a single line of communication.
Here, there are multiple processes running on a single host, and they
need to share the host's network layer service.

This is done using port numbers.

.. admonition:: Example

    Last week, I was working on a project, using my Laptop and a
    Raspberry Pi.
    The pi was "headless", which meant that there was no
    display, keyboard or mouse connected to it. 

    I needed to connect to pi using SSH. I also needed to access a
    website running on the pi. I do so as follows,

    * I connect to the raspberry pi by opening a terminal and typing
      ``ssh pi@192.168.1.100``
    * I connect to the website by opening chrome and typing
      ``http://192.168.1.100/`` in the url bar.

    The two commands above contain a lot of info,

    * http:// - Tells transport layer that (default) destination port is
      TCP 80.
    * ssh - Tells transport layer that (default) destination port is
      TCP 22.
    * 192.168.1.100 - Destination IP passed on to network layer
      (for both commands)

    The transport layer service (which is part of the OS), takes the
    data that the application wants to send,

    * adds a source and destination port
    * optionally add other things, like checksums etc.

    and sends it off to the network layer service.

    The packets reach the other side, to the raspberry pi's network
    layer service. Here,

    * the additional things like checksums are used for
      error-correction (if they exist).
    * the destination port is used to understand which application this
      is meant for

    and the data is sent up to the application.