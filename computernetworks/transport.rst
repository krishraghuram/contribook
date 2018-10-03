Transport Layer
===============
	
	*We will cover Transport Layer in more
	detail than any other layer.*

Interaction between Application Layer and Transport Layer
---------------------------------------------------------

Introduction
^^^^^^^^^^^^

The transport layer provides logical communication between applications.

The application does not need to bother about the network.
Transport Layer "abstracts away" all networking stuff.

To the applications - both client and server side -
it is as if they are communicating to each other directly,
as if they were running on the same system.

But to achieve this, the application needs to provide some details.

* Destination IP
* Destination Port
* Source Port
* Source IP

Usually, the Transport Layer can safely assign a unused source port.
It can also get source ip from the network layer service or operating system.
Thus, the Destination IP and Port are the crucial details
that the application must provide. 

Recall sockets - The interface between application and transport
layer - During creation of a socket, the application has to specify
these details. 

Example
^^^^^^^

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

Interaction between Transport Layer and Network Layer
-----------------------------------------------------

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

Multiplexing and Demultiplexing
-------------------------------

We need to provide process-process communication from host-host
communication.

According to wikipedia, "multiplexing is a method by which multiple
analog or digital signals are combined into one signal over a
shared medium".

How is this done???

It is very simple. We use the port numbers.

Example
^^^^^^^

Last week, I was working on a project, using my Laptop and a
Raspberry Pi (issued from Robotics Club). 
The pi was "headless", which meant that there was no
display, keyboard or mouse connected to it. 

To access the pi, I need to SSH into it.

It is also impossible to work on any project without
stackoverflow or google. 

I connect to both as follows,

* I connect to google by opening chrome and typing
  ``http://216.58.199.163`` in the url bar.
* I connect to the raspberry pi by opening a terminal and typing
  ``ssh pi@192.168.1.100``

.. note::
	For the sake of sticking to Transport Layer concepts -
	I cheat a little bit.
	I don’t actually type http://www.google.co.in.
	Instead, I first do a DNS lookup for www.google.co.in,
	and find the IP to be 216.58.199.163.
	Then I type http://216.58.199.163

The two commands above contain a lot of info,

* http:// - Tells transport layer that (default) destination port is
  TCP 80.
* ssh - Tells transport layer that (default) destination port is
  TCP 22.
* 216.58.199.163 - Destination IP passed on to network layer
* 192.168.1.100 - Destination IP passed on to network layer

Most operating systems provide support for networking,
especially TCP/IP. This usually runs as part of the
"networking service" that the OS provides.

Thus, TCP, which is part of the "networking service",
basically collects data from both Chrome and Terminal,
packetizes the data, and adds the Source IP, Source Port,
Destination IP and Destination Port to each packet.

Since Source Port is not specified by either application,
TCP assigns random unused source ports by itself.

Since Source IP is not specified by both chrome and terminal,
TCP gets this from "networking service" of the OS.

Destination Port and IP are specified by both chrome and ssh.

When the packet reaches google's server, the "networking service" on
the server sees the port number, and sends it to the application
*listening* on port 80.

