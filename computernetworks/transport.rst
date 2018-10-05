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

.. note::

    The above explanation considers just one instance of a "application
    communicating with another application". In reality, networks are
    much more complex.

    To give an idea, each host will have multiple applications using the
    network, to send and receive data,
    from various other hosts in the network.

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
    any physical connection, such as copper/optical cable or wireless
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

.. todo::
    Continue from here.

Multiplexing and Demultiplexing
-------------------------------

We need to provide process-process communication from host-host
communication. Let's see what is interesting about this problem.

The transport layer service on the receiver gets packet from
the network layer below. How does it know what application is the
intended receiver of the packet?

Thus, it needs some extra information, which allows it to
decode/decipher the intended receiving application.

The transport layer service on the sender has to provide this extra
information.

**Ports and Port numbers**



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

