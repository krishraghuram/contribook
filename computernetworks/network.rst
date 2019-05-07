Network Layer
=============

.. note::
    Though this page is titled "Network Layer", we will only discuss one
    protocol in the Network Layer - IP, the Internet Protocol

    There are a few other protocols in layer 3, mentioned `here
    <https://en.wikipedia.org/wiki/List_of_network_protocols_(OSI_model)
    #Layer_3_(Network_Layer)>`_.
    
    But most of them aren't of interest to us... The one's that are
    somewhat interesting are

    * IP (v4 and v6)
    * ICMP
    * ARP
    * NAT

    The remaining protocols are either obsolete, or used only in proprietary
    or closed source softwares.

    Also, among the ones listed above, IP is the most-well known to normal
    users. This is because both TCP and UDP use IP as the underlying network
    layer protocol.

.. note::
    Often, the protocols used in the working of the internet are
    termed the `Internet Protocol Suite`_

.. _`Internet Protocol Suite`:
    https://en.wikipedia.org/wiki/Internet_protocol_suite

Internet Protocol
-----------------

Brief History
^^^^^^^^^^^^^

The internet protocol defined a unique address for each network interface -
termed IP address.

IPv4 has address length of 32 bits.
These are often described using dotted-decimal notation,
a.b.c.d, with a,b,c,d being from 0-255.

Originally, this was split into 8 bits for identifying the Network (Network ID)
and 24 bits for identifying the Host inside the network (Host ID).
However, people soon realized that we need more than 256 networks.

Thus, people worked on clever ways to allocate the IP addresses.

**Classful Networking**
In this, they defined 5 classes of networks, A, B, C, D and E.
Depending on the no. of hosts in your network,
you can *buy* a network from any of the classes A, B or C.

**Classless Inter Domain Routing**
Even classful networks were not good enough.
Thus, the Classless Inter Domain Routing(CIDR) system was defined.
This system allowed for hierarchical division of networks,
and gave freedom to network administrators to subdivide networks as they wish.

IPv4
^^^^

Today's IPv4 used Classless Inter Domain Routing for allocating IP addresses.

