Transport Layer
===============
    
    *We will cover Transport Layer in more
    detail than any other layer.*

Interface between Application Layer and Transport Layer
-------------------------------------------------------

The transport layer provides logical communication between applications.
It *abstracts away* the lower level details from the application.

In other words, to the application processes, it looks as if they are 
communicating directly. While in reality, they might be on opposite
sides of the world.

.. image:: ../_images/sender_receiver.svg
   :width: 50%
   :align: center

On the sender, the application sends the data to the transport
layer service, which processes the data, and sends it
down to the network layer service.

The network layer is responsible for sending the packets to the
destination machine.

On the receiving side, the network layer passes the packets to
the transport layer service, which passes it to the appropriate
application.

The two most popular transport layer protocols on the internet stack
are,

1. TCP (Transmission Control Protocol)
2. UDP (User Datagram Protocol)

.. note::

    The above explanation considers just one instance of a "application
    communicating with another application". In reality, networks are
    much more complex.

    To give an idea, each host will have multiple applications using the
    network, sending and receiving data
    from various other places in the network.

.. note::

    The transport layer service and network layer service are almost
    always part of the Operating System.

    Thus, for a host, there is only one transport layer service and one
    network layer service.

########################################################################

Interface between Transport Layer and Network Layer
---------------------------------------------------

Transport Layer provides **logical communication between processes**.
Network Layer provides **logical communication between hosts**.

The distinction is subtle, but it is important.
Read more from Kurose and Ross Section 3.1.1

.. image:: ../_images/transport_network.svg
   :width: 75%
   :align: center

.. note::

    The image is only for understanding, and does not represent
    any physical connection, such as copper cables or wireless
    signals.
    
    The *physical* connection between the hosts might be very different
    from the *logical* connection that the network layer or transport
    layer sees.

########################################################################

Recap
-----

Transport Layer Protocols have the task(s) of,

* Providing a process-process communication
  using a host-host communication.
* Additionally, choose to provide services such as,

    * Error Detection and Correction
    * Reliable Data Transfer
    * In-Order Arrival
    * Flow and Congestion Control

########################################################################

Multiplexing and Demultiplexing
-------------------------------

We need to provide process-process communication from host-host
communication.

There might be multiple applications running on a host machine. When
the transport layer receives data from network layer below, it needs to
which application to send it to.

Recall Sockets and Ports from Application Layer. Ports are used by
transport layer to uniquely identify applications and Sockets are used
to transfer data to/from application.

Example
^^^^^^^

**On my laptop I,**

* SSH into my VM on digitalocean by opening a terminal and running
  the ssh command : `ssh user@139.59.100.100`
* Open chrome, and goto google : `https://www.google.com`

The applications, do the following.

* The ssh command knows that default port of ssh protocol is 22. Since I
  didn't explicitly specify a different port, 22 will be used.
* Chrome knows that default port of https protocol is 443.  Since I
  didn't explicitly specify a different port, 443 will be used.
* Usually, client applications do not specify source port. Rather, the
  transport layer assigns a random, unused source port by itself.

The transport layer service running as part of the linux kernel does
the following,

* Adds a header to all packets containing source and destination
  ports.
* Optionally, depending on the transport layer protocol, it might do
  some other things like error correction etc.
* Passes on the packet to the network layer.

The network layer sends the packets meant for google to google's
webserver, and the packets meant for ssh to digitalocean's VM.

**On google's webserver**

The network layer receives the packets and sends them to the transport
layer.

The transport layer sees that the destination port is 443, so it sends
the packet to the application listening on that port. Usually, this is
a webserver like nginx, but you can't say that about google. They
customize everything.

The webserver serves the index.html page.

How does it know where to send?

The source ip and source port from our original request are used for
this purpose.

**On digitalocean's VM**

The network layer receiving the packets, and sends them to the transport
layer.

The transport layer sees that the destination port is 22, so it sends
the packet to the openssh server running on port 22.

The SSH sends back a reply, asking us to authenticate with the password.

How does it know where to send?

The source ip and source port from our original request are used for
this purpose.

Connectionless Mux-Demux
^^^^^^^^^^^^^^^^^^^^^^^^

In UDP, there is no connection between source and destination.

The UDP packet is completely identified by the destination ip and port.

Thus, packets from different source ips and ports will be sent up the
same socket by the transport layer of the receiving host.

It is the application's responsibility to distinguish different sources,
and send appropriate replies.












The sending machine's transport layer would have added a
**destination port** to the header of the packet.
The receiving machine's transport layer forwards the
packet to the application running on that port.

What if the receiving machine's application wants to send a reply?

Exactly for this need, the sending machine's transport layer also adds
a source port to the header.


On the sending end, the transport layer receives data from applications,
which are to be sent across the network.
The transport layer service adds header containing
source and destination ports.

On the receiving end, the transport layer service receives data from
network layer, looks at the destination port, and sends the packet to
appropriate application.

Thus, the port numbers are used for Multiplexing and Demultiplexing.

.. note:: What is the use of sending the source port?

    The source port serves as a "From" address.
    Without it, the receiver won't be able to reply back.

