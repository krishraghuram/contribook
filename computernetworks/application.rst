Application Layer
=================

Client-Server Architecture
--------------------------

Links
^^^^^

* `2 minute video on client-server model`_
* `6 minute video, that explains some parts better`_

.. note::
	The second video is kind of vague about "virtual servers"
	- so please ignore that.

Thought client-server model is the most widely used, it is not the only
 one. There are other models too. Specifically,

.. todo::
	Expand Peer-to-Peer and Publisher-Subscriber models.

* Peer-to-Peer model
* Publisher-Subscriber model

.. _`2 minute video on client-server model`:
	https://www.youtube.com/watch?v=SwLdKeC8scE	

.. _`6 minute video, that explains some parts better`:
	https://www.youtube.com/watch?v=L5BlpPU_muY

Key Points
^^^^^^^^^^

* Client initiates the connection
* Server is always waiting for clients
* Server responds to Client’s requests
* This is called the Request-Response cycle

########################################################################

Basics of Network Addressing
----------------------------

IP Address - is a 32 bit number used to uniquely identify a host
system(computer).

Port - is a number that uniquely identifies a process on a host.

Together, a given IP and Port uniquely identify a application running
on a host in a network.

We will discuss IP Addresses and Ports in greater detail when we get to
Network Layer and Transport Layer.

########################################################################

Sockets and Ports
-----------------

The application layer work is done by the code in the application. 
The transport layer work is done by services running on the Operating
System.

Socket is a 'software entity' that acts as the interface between
Application and the Operating System. Therefore, Socket is like a
doorway between Application and Operating System - passing packets from
Application to OS and vice-versa.

Equivalently, we can call Socket as the interface between Application
Layer and Transport Layer.

Ports and Sockets are very closely related. 
Ports are used to uniquely identify a process.

A Socket is the software interface between Application Layer and
Transport Layer. An application layer process interacts with the
transport layer processes using a socket. During the creation of this
socket, a port must be specified, so that the application can be
uniquely identified later.

For all intents and purposes, you can consider Ports and Sockets to be
the same.

########################################################################

Transport Layer Protocols available to Application Layer
--------------------------------------------------------

The two most popular Transport Layer protocols available to applications
are,

1. TCP - Transmission Control Protocol
2. UDP - User Datagram Protocol

Application Layer protocols are free to choose either.

The choice depends on the differences between the services that TCP
and UDP offer. We will look at this in detail in Transport Layer.

########################################################################

HTTP
----

HTTP - Hyper Text Transfer Protocol

HTTP began with the Tim Berners-Lee and World Wide Web.

HTTP is stateless

Google, Youtube, Facebook - are all Websites served through HTTP.

Links
^^^^^

* `What is HTTP?`_
	
	Personally, I'm not a fan of the 'kitchen' or the 'coin' examples,
	but whatever works for you man.

.. _`What is HTTP?`:
	https://www.youtube.com/watch?v=SzSXHv8RKdM


Key Points
^^^^^^^^^^

* Works using Client - Server model, and thus,
  through Request - Response cycles
* Based on TCP/IP
* Default server port - TCP Port 80 (Don’t have to memorise)
* Stateless - Server forgets about client after the response.
* Request Methods and Response/Status Codes

	* Request Methods define the action that the client wants to
	  perform. For example,

		* GET
		* POST
		* HEAD

	* Status code is a short 3-digit code which tells the result of the
	  request. For example,

		* 200 - OK
		* 404 - Not Found
		* 403 - Forbidden
		* 407 - Proxy Authentication Required

Side Joke
^^^^^^^^^

.. image:: ../_images/httpresponsecodejoke.jpg
   :width: 50 %
   :align: center

Extras
^^^^^^

In no particular order,

* `Wikipedia - HTTP`_
* `HTTP Response Codes as Valentine’s Day Comics`_
* `Steve's Internet Guide - HTTP`_
* `Slides from NTU`_
* `Mozilla Developers aka MDN - Collection of Articles on HTTP`_
* 'How the Web Works' - Series of posts on Medium

	* `How the Web Works - 1`_
	* `How the Web Works - 2`_
	* `How the Web Works - 3`_

.. _`Wikipedia - HTTP`:
	https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol

.. _`HTTP Response Codes as Valentine’s Day Comics`:
	https://medium.com/@hanilim/http-codes-as-valentines-day-comics-
	8c03c805faa0

.. _`Steve's Internet Guide - HTTP`:
	http://www.steves-internet-guide.com/http-basics/

.. _`Slides from NTU`:
	http://www.ntu.edu.sg/home/ehchua/programming/webprogramming/
	http_basics.html

.. _`Mozilla Developers aka MDN - Collection of Articles on HTTP`:
	https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP

.. _`How the Web Works - 1`:
	https://medium.freecodecamp.org/how-the-web-works-a-primer-for-
	newcomers-to-web-development-or-anyone-really-b4584e63585c

.. _`How the Web Works - 2`:
	https://medium.freecodecamp.org/how-the-web-works-part-ii-client-
	server-model-the-structure-of-a-web-application-735b4b6d76e3

.. _`How the Web Works - 3`:
	https://medium.freecodecamp.org/how-the-web-works-part-iii-http-
	rest-e61bc50fa0a

########################################################################

Cookies
-------

HTTP is stateless. 

The server forgets about the client after each request-response cycle.
When the client sends another request,
the server does not know about the previous request-response.

So... http servers are a bit like
`10 second Tom <https://www.youtube.com/watch?v=6kbY9rGTgQo>`_.

Then how does google and facebook “remember” that we are logged in?

The answer is cookies.

Links
^^^^^

* `Wonderful Video - What is a cookie?`_

* `Cookies explained using Starbucks Analogy`_

.. _`Wonderful Video - What is a cookie?`:
	https://www.youtube.com/watch?v=I01XMRo2ESg

.. _`Cookies explained using Starbucks Analogy`:
	https://www.youtube.com/watch?v=64veb6tKTm0

Key Points
^^^^^^^^^^

Cookies are identifiers that are given by web-servers when you visit
them for the first time. On subsequent visits to the same website, your
browser sends the cookies along with the http request. This allows the
website to recollect who you are, what did you do last time etc.

Cookies is what allows for Stateful HTTP.

You can disable cookies in your browser. This increases your security,
but you will have to login into gmail and facebook every single time you
open them. Typically, I take the middle ground of just disabling
"third-party" cookies.

Extra - Cookies and Sessions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Cookies can be of two types:

1. Pure Client Side Cookies
   
   Here, all the info that server needs about user, is stored on the
   cookie itself and sent to the user.

   Advantage - Server doesn't have to perform a 'look-up' each time.
   Disadvantage - Security loopholes, Limited size etc.

2. Cookies + Server Side Sessions
   
   Here, cookies are used just as unique identifiers, and the actual
   info about user is stored on the server. The server looks up this
   info using the cookie aka. unique identifier.

   Advantage - Unlimited Size.
   Disadvantage - Server has to perform a look-up on each request.

########################################################################

Web-Cache/Proxy-Server
----------------------

What is caching?
^^^^^^^^^^^^^^^^

Caching is the process of saving something at a closer location on the
first read, so that subsequent reads are faster.

It is not limited to computer networks, and is used in other places too.

* For example, it is used in computers, where RAM is a cache
  for theHard-Disk/SSD. Processors have their own cache,
  which cache the RAM.
* Redis, MemcacheD etc. can cache things like Database requests.
* Lastly, we have Web-Caches which cache HTTP requests. Proxy Servers
  are one way to implement a Web-Cache.

Links
^^^^^

Both links are extremely good.

* `What is a Proxy Server?`_
* `What is caching?`_

.. _`What is a Proxy Server?`:
	https://www.youtube.com/watch?v=qU0PVSJCKcs

.. _`What is caching?`:
	https://www.youtube.com/watch?v=o2KMk_TyC8E

########################################################################

HTTPS
-----

HTTP - sends data as plain text

Not a good way to send stuff like Passwords, Credit Card Info etc.


Link
^^^^

* `Robert Heaton - How does HTTPS actually work?`_

.. _`Robert Heaton - How does HTTPS actually work?`:
	http://robertheaton.com/2014/03/27/how-does-https-actually-work/

Above link is not a short and sweet video like others. That’s because
videos do not contain detailed information. At least, not the ones
under 10 minutes. So, it’s usually better to read up content from
books, webpages, blogs, wikipedia pages, man pages of commands etc.

########################################################################

SSH
---

.. todo::
	Improve SSH Notes

Link
^^^^

* `Intro to SSH`_

.. _`Intro to SSH`:
	https://www.youtube.com/watch?v=mF6J-VQHPxA

SSH is extremely useful

The thing is, SSH is extremely useful,
but most people don't need the "inner workings" of it.

To work with SSH practically, you need a SSH server and a SSH client.

Most Linux distros come with ssh command line client.
You can test this on terminal by typing "which ssh".
For windows, you have Putty - but I do not recommend this,
as working with SSH keys is a pain on Putty.

For the server, goto some popular cloud provider, 
be it Digitalocean, GCP, AWS or Azure, and get a Virtual Machine.
Most providers provide a "free-tier". Set up SSH.

Search and Learn :

1. Login
2. Setup SSH Keys
3. Disable Password Based Authentication
4. Use SCP or RSYNC to transfer files

RSYNC
^^^^^

rsync is an alternative to scp, and has some really cool options.

1. Copy only files that have changed.
2. Copy, but preserve stuff like modification times, owners,
   permissions etc.
3. Seamlessly compress and decompress files during the copy, to reduce
   network usage.
4. Delete files in destination, that are not present in source.

.. note::
	I often use rsync to backup files to external hard disk.
	The command I usually run is,
	``rsync -azP /home/raghuram /run/media/hard-disk/``
	Note that the command does not have any remote ip's.
	In fact, it does not even use the network.
	I use it over, rather than simple ``cp``, because of the its
	features.

########################################################################

DNS
---

DNS is probably the most important protocol for humans to use internet.

The below links explains DNS in a very layman way,
without digging deep into how each query happens.

Note that they might be using slightly simplified terminology to make
the explanation shorter.

Links
^^^^^

* `DNS Made Easy Videos - DNS Explained`_
* `Techquickie - DNS as Fast As Possible`_

.. _`DNS Made Easy Videos - DNS Explained`:
	https://www.youtube.com/watch?v=72snZctFFtA

.. _`Techquickie - DNS as Fast As Possible`:
	https://www.youtube.com/watch?v=Rck3BALhI5c

Some of you probably wanted more in-depth info.
Don't worry, I have you covered.

* Kurose and Ross - Section 2.5
* `Wikipedia Page of DNS`_

.. _`Wikipedia Page of DNS`:
	https://en.wikipedia.org/wiki/Domain_Name_System

Key Points
^^^^^^^^^^

* DNS is a application level protocol. It uses UDP for its transport
  layer functionality.

* Computers need IP addresses to find things on internet. 
  Humans like to use names. DNS is the complex system that translates
  names to addresses. 

   If DNS wasn’t envisoned, we would all be maintaining a
   small notebook, much like the phone directory of the landline days. 

* DNS is distributed - the translation table is not stored at any
  single location.

* DNS is a hierarchical protocol.

   * For example, when I want to go to google.com, my browser asks
     IITG’s DNS server 202.141.81.2. 
   * If the server has the IP for google.com in its cache, it will give
     it to me.
   * But if it does not, it will ask a higher level DNS server for
     the IP.
   * This process can repeat until we reach the Root DNS servers,
     and finally find the IP.

* DNS replies are cached.
   
   * The first time you load google.com, you possibly started a
     domino chain of requests up to the internet’s root dns servers.
   * Imagine the same thing happening on every refresh - the root dns
     servers will not be able to handle the number of requests from the
     billions of devices connected to the internet.
   * To reduce load on higher level servers, and to reduce network load
     in general, DNS replies are cached. This means that everyone in
     the domino chain stores the ip of google.com for a while,
     including your browser.

* Domain Names are purchased through registrars. Read more at,

	* `Beginners Guide to Domain Names`_
	* `Beginners Guides to various activities of ICANN and IANA`_
	* `Main website of ICANN`_

.. _`Beginners Guide to Domain Names`:
	https://www.icann.org/en/system/files/files/domain-names-
	beginners-guide-06dec10-en.pdf

.. _`Beginners Guides to various activities of ICANN and IANA`:
	https://www.icann.org/resources/pages/beginners-guides-2012-03-06-en

.. _`Main website of ICANN`:
	https://www.icann.org/

########################################################################

NTP
---

NTP is not very popular,
and most courses on networks wouldn’t mention it.
But I think that it deserves at least one slide,
considering we have talked so much about DNS.

Key Points

1. NTP, or Network Time Protocol,
   is what allows humans to maintain time across the globe.
2. Like DNS, NTP is also hierarchical.

	* The root time servers (called Stratum 0 servers) are the
	  Atomic Clocks that use Caesium for measuring time -
	  as defined in the SI unit of second. Isn't that cool?

.. figure:: ../_images/ntp.jpg
   :width: 50 %
   :align: center
   
   A Stratum 0 NTP server of US Naval Observatory, located in Colorado.
   Read more `here <https://en.wikipedia.org/wiki/File:Usno-amc.jpg>`_

Read more at,

Links
^^^^^

* `Wikipedia Page of NTP`_
* `NTP Project Page`_

.. _`Wikipedia Page of NTP`:
	https://en.wikipedia.org/wiki/Network_Time_Protocol

.. _`NTP Project Page`:
	http://www.ntp.org/ntpfaq/NTP-s-def.htm

.. note::
	Want to implement your own Stratum 0 NTP server with Raspberry Pi?

	http://rdlazaro.info/compu-Raspberry_Pi-RPi-stratum0.html

########################################################################

DHCP
----

.. todo::
	Expand DHCP

Most of us never set Static IP Addresses. We connect to a wifi network,
and everything just works. 

All thanks to DHCP - Dynamic Host Configuration Protocol.

We have decided to take a leaf from the book of mathematicians and
leave DHCP as an exercise to the reader.

Search online, find some content, and learn yourself.
