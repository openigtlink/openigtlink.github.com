---
layout: page
title: For Developers
group: navigation
order: 3
description: ""
---
{% include JB/setup %}


The OpenIGTLink protocol defines a set of message formats for several data types
that are frequently used for image-guided and robot-assisted interventions.
Those formats are used to compose messages that are transferred from one device
to another over the local area network. The application developers can choose
their own transportation layer that fits for their application and environment
(e.g. TCP, UDP, WebSocket).


--------------------------------------------------------------------------------

Protocol Specifications
=======================

See [Protocol Specification Page](spec) for detail.


--------------------------------------------------------------------------------

Software Development Kits (SDKs)
================================

To use OpenIGTLink in your software application, you need to either:
1) implement serialization/de-serialization of messages by your self, or
2) use existing libraries. C/C++ and Java libraries are currently available
as free open-source software.


C/C++
-----

See [OpenIGTLink C/C++ Library Page](cpplib) for detail.

We provide [the OpenIGTLink C/C++ library](cpplib)
as free open-source software under the BSD-style license. The OpenIGTLink library
provides application program interface (API) to communicate with other software
over the network. The OpenIGTLink library supports major platforms including
Microsoft Windows, Linux, and macOS (Mac OS X). Those open-interface and 
multi-platform strategies will lead to the widespread use of OpenIGTLink, and
ultimately help to establish the interoperability among a wide variety of
components developed by different groups and companies in the community.

Java
----

AIM Lab at Worcester Polytechnic Institute is providing Java implementation of
OpenIGTLink library as free open-source software. Please visit:

* [http://aimlab.wpi.edu/research/projects/OpenIGTLink_Interface](http://aimlab.wpi.edu/research/projects/OpenIGTLink_Interface)
* [http://code.google.com/p/igtlink4j/](http://code.google.com/p/igtlink4j/)

for more detail.


Other Languages
---------------

There is no official implementation of OpenIGTLink interface in other language.
However, developers can use OpenIGTLink from the Python environment on 3D Slicer.
See [3D Slicer OpenIGTLinkIF Developers' information](https://www.slicer.org/wiki/Documentation/Nightly/Developers/OpenIGTLinkIF).


Development and Maintenance
===========================

The OpenIGTLink protocol is developed and maintained at by the OpenIGTLink
community hosted at National Center for Image Guided Therapy, Brigham and Women's Hospital.
OpenIGTLink protocol is an open-source project; anyone is welcome to join the development.

The project is hosted at GitHub. There are several ways to participate the project:

Report Bugs / Request Features
------------------------------

If you find any issues or have feature request, please feel free to post to Issues in
[GitHub Issues](https://github.com/openigtlink/OpenIGTLink/issues).

As for feature requests, please note that we may not incorporate requested features
into the protocol, in order to maintain the compatibility of the protocol
with existing software/hardware. 

Contribute Patches
------------------

The OpenIGTLink community is adapted to the collaborative development model on GitHub.
[GitHub's instruction](https://help.github.com/articles/about-collaborative-development-models/)
provides a very nice overview of collaborative development models and workflows.

Participate Project Weeks
-------------------------

There have been groups of people who organize small projects related to OpenIGTLink
at biannual [Project Week] hosted by National Alliance for Medical Image Computing.
Project Week is a hack-a-thon event focused on development of software platforms for
medical image computing and computer assisted intervention. Please check [Event](/events/)
page or contact [Junichi Tokuda](http://www.spl.harvard.edu/pages/People/tokuda) for the future projects.





