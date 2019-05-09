Network Layer
=============

.. note::
    Often, the protocols used in the working of the internet are
    termed the `Internet Protocol Suite`_

.. _`Internet Protocol Suite`:
    https://en.wikipedia.org/wiki/Internet_protocol_suite

Internet Protocol v 4
---------------------

The network layer has the job of providing a logical connection between hosts.
The internet protocol does this for the internet.

.. note::
    Today, the Internet Protocol is so widespread, that it is also used for most
    Local Area Networks (with some minor differences).

How does it work?
At the heart of the protocol is the IP Address -
a unique address to every network interface connected to the internet.

Every computer connected to the internet has to have a network interface.
This is most probably the LAN port or the WiFi card.
This network interface is assigned a unique 32 bit address called IP address.

It is usually written in dotted-decimal representation, as a.b.c.d,
where a,b,c,d are in the range 0-255.

IP Address Allocation
^^^^^^^^^^^^^^^^^^^^^

Allocating unique addresses is a deceptively complicated problem.

Firstly, how do we ensure that there aren't any collisions?

It is impossible for any one person or organisation to maintain a list of size
2^32. Even if it is possible, it won't be efficient.

Thus, they delegated the problem.
Let the first 8 bits identify the network, and the remaining 24 bits identify
the host within the network.
There would be maximum 256 networks, and maximum of 2^24 hosts inside each
network.
Each network is responsible for allocating addresses to its hosts.

Classful Networking
^^^^^^^^^^^^^^^^^^^

The original IP address allocation scheme had fixed 8 bits to identify the
network and 24 bits to identify the host within the network.

But very soon, it was realized that 256 networks were not sufficient,
and not every network needs 16,777,216  addresses.

Thus, the address space was redistributed into "classes" - A, B, C, D and E.

D was reserved for multicast use, and E was reserved for any future needs.

Class A addresses started with a "0", then a 7 bit network id, and then 24 bit
host id.

Class B addresses started with "10", then 14 bit network id, and then a 16 bit
host id.

Class C addresses started with "110", then 21 bit network id, and then a 8 bit
host id.

Thus,
Class A has 128 networks of size 16,777,216
Class B has 16,384 networks of size 65,536
Class C has 2,097,152 networks of size 256

Which is a much better system than having 256 networks of size 16,777,216.

Subnetworks
^^^^^^^^^^^

In above cases, the internet is viewed as a two-tier network.

The internet contains many networks, and each network contains many hosts.

But as computers became widespread, organizations wanted to have a two-tier
hierarchy themselves, as that would make many things simpler.

After lot of thinking and proposals, Subnets came to picture.

Everything is same as the classful scheme explained above, except that the
host id can now be split into a subnet id and host id.

The subnet id identifies a subnetwork within the network, and the new host id
identifies a host within that subnetwork.

What is the length of the subnet id?
Well - this is the clever part. Instead of having fixed classes like above,
they decided to have a "bitmask".
The positions of the bitmask which are "1" will identify the subnet id in the
IP address.

This allows for organizations to choose how it wants to distribute its subnets
hosts. One could do anything from having few subnets with many hosts in each,
to having many subnets with few hosts in each.

This was named Variable Length Subnet Masking (scientists love to complicate
the names of simple things)

Classless Inter Domain Routing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Often abbreviated as CIDR, is the next step in the evolution of the internet.
Before this, we had,

* Classful networks with classes A, B and C
* Subnets with variable length bit masks

CIDR does the following:

* Abolish the networks classes A, B and C

* Instead, divide up the internet into subnets, with each subnet having a
  "IP prefix".

* Further, each subnet can be subdivided indefinitely into more subnets,
  where the IP prefix of each subnet is created by adding bits to the IP prefix
  of its parent subnet.

* Lastly, in the context of CIDR, they are not called "subnets". Instead, they
  are called CIDR blocks.

Notation and Example:

CIDR notation is a compact representation of an IP address and its routing
prefix. A slash is used to separate the IP address from prefix length.

For example, in `192.168.100.14/24`, the `192.168.100.14` is the IP address,
and the first 24 bits of the IP address give us the routing prefix.

`255.255.255.0` would be the equivalent subnet mask for the prefix length `24`.

The CIDR notation may be used to represent a single interface, or it could be
used to represent a whole block of addresses.

For example, `192.168.100.14/24` represents the IP 192.168.100.14, with a prefix
of (length 24) 192.168.100.0

`192.168.100.0/24` represents a block of addresses starting from `192.168.100.0`
to `192.168.100.255`

Why was this done?

* More flexibility and control to network administrators, since they can freely
  divide up the CIDR blocks.

* Common prefix reduces the amount of routing information to be shared between
  routers and gateways.

.. note::
    Subnets before CIDR were supposed to be only of one level. That is, there
    were no sub-subnets.
    In CIDR, each block can be subdivided into more blocks, as long as we stick
    to the 32 bit length limit of IP addresses.

