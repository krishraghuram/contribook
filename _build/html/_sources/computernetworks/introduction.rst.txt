Introduction
============



How to use this course?
-----------------------

Excerpt from Arch Wiki, 

	*Most articles on the ArchWiki do not attempt to provide a holistic introduction to a single topic; they are instead written in adherence to the DRY principle, under the assumption that the user will seek out and read any supporting material that they do not yet understand.*

This microcourse mostly **points** to good resources, as there is already sufficient content on the internet.
You'll find a curated list of blogs, videos and notes inside.

Computer's are much better than us in storing and reproducing content. Humans are unique because we can ask the **bigger questions**.
Thus, there is also additional narrative in this course, that forces the reader to take a step back, and ask the bigger questions. 

.. note::
	For those who want a more traditional book, check out - "Kurose and Ross - Computer Networking, A Top-Down Approach"

.. note::
	Wikipedia is good for in-depth info. The only thing probably better than the Wikipedia pages are the RFCs themselves.

###############################################################################

The Internet Network Stack
--------------------------

The TCP/IP stack divides network protocols and concepts into 5 *conceptual* layers.

1. Application Layer
2. Transport Layer
3. Network Layer
4. Link Layer
5. Physical Layer

Why did they do this?
^^^^^^^^^^^^^^^^^^^^^

To understand that, we have to ask ourselves, "What is required/expected of 'computer networks'?"

* The networks should allow for **communication** between computers
* We expect the networks to be **reliable**, **error-free**, **fast** and **easy-to-use**. What's the point of a new technology, if it's no better than existing ones like radio, telegraph etc.

The terms in bold above, are vague, and thus, the problem is of a **very broad scope**.

To give an idea of how broad, here is a list of sub-problems that all fall in the above umbrella. 

* How can we send data from one computer to another, without errors?
* Computers understand numbers, and thus, *addresses* are stored as numbers. But humans are not good at remembering long numbers, so how can we build a *translator* between names to numbers?
* How can we build an application that allows video-conferencing? 

Humans are not meant to think and work on such a broad scope.
Thus, we **split** the problem into parts and work on the parts **independently**.
That is why we people have defined logical layers in networking - so that we can
independently work on improving each layer, without having to worry about others.
They are able to do this because the **interface** between each of the layers is
well-defined. 

###############################################################################

What is a "Protocol"?
---------------------

In layman terms, a protocol is a language. Just like English and Hindi.

**The difference - protocols have much less ambiguity in their statements.**

Computers cannot work with ambiguous statements - they don’t have the cognitive
capabilities that we do.

Remember this programmer joke?

.. image:: ../_images/milkeggs.jpg
   :scale: 65 %
   :align: center

Some Example Protocols
^^^^^^^^^^^^^^^^^^^^^^

1. HTTP, SSH, DNS, NTP, DHCP - Application Layer Protocols
2. TCP, UDP - Transport Layer Protocols
3. IP, ICMP - Network Layer Protocols
4. ARP, Ethernet - Link Layer Protocols

We will cover each in detail over the course.

###############################################################################

Links to Read
-------------

* https://www.youtube.com/watch?v=zyL1Fud1Z1c
* https://www.youtube.com/watch?v=Pje0l5r7_lk
* https://www.youtube.com/watch?v=PpsEaqJV_A0 - Ultra Basic Video
* https://www.youtube.com/watch?v=VlKks__ZhI0 - Ultra Basic Video

The first two probably confused you with 5 Layer Internet Stack vs 7 Layer OSI Reference Model. In that case, this might help :

* https://en.wikipedia.org/wiki/OSI_model#Comparison_with_TCP.2FIP_model
* https://en.wikipedia.org/wiki/Internet_protocol_suite#Comparison_of_TCP.2FIP_and_OSI_layering

In case that confused you even more, read the next section. I promise I'll clarify this.

OSI vs Internet
^^^^^^^^^^^^^^^

* The OSI Model was created by International Organization for Standardization or ISO.
* The internet as it is today, was developed by several thousand(or more) different people. No single person or entity can be credited for creating the Internet.
* The people who worked behind it, took the OSI Model as a reference, and built Internet’s structure based on same principles. **In this process, they dropped two layers - which they thought were not necessary.**
* So.. who will perform the jobs of these layers? - If an application needs the services that these layers provided, let the application developer write his own code.
* Throughout this course, we work with 5 layer internet stack. So you can forget the OSI Reference Model.
