---
layout: page
title: For Developers > Specification
header: Pages
weight: 2
---
{% include JB/setup %}

Introduction
============

The protocol description is maintained as part of source code for [the C/C++ library](https://github.com/openigtlink/OpenIGTLink.git). Please refer to [OpenIGTLink Protocol Description in GitHub](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/index.md) for the up-to-date description.

OpenIGTLink is an open-source network communication interface specifically
designed for image-guided interventions. It aims to provide a plug-and-play
unified real-time communications (URTC) in operating rooms (ORs) for image-guided
interventions, where imagers, sensors, surgical robots,and computers from
different vendors work cooperatively. This URTC will ensure the seamless data
flow among those components and enable a closed-loop process of planning, control,
delivery, and feedback. The specification of OpenIGTLink is open, and can be
used without any license fee; hence OpenIGTLink is suitable for both industrial
and academic developers. 

Since the OpenIGTLink project stated in 2007, three major revisions have been
made to the protocol. Most of the OpenIGTLink interfaces currently available
comply with version 2 protocol. Please refer to the following pages for
detailed specification of each version of the protocol

- [Release 2.0](protocols/v2_index.html)

- [Release 3.0](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/index.md)

[AUTO_VER2]: <> (DO NOT CHANGE THIS LINE. The release script will add a release log here.)


What's New in Version 3
=======================

We are currently undergoing a transtion from version 2 to 3.x. At past sevral
[Project Weeks](https://www.na-mic.org/Wiki/index.php/Project_Events#Past_Project_Weeks),
a group of application developers from several institutions got together and discussed
the limitations in version 2, and drafted an extended protocol, which was later 
released as version 3. The following changes have been made:

- A new message structure. The body in the former protocol was splitted into extended header, content, and metadata. The message now consists of the following sections:
  - Header (58 bytes)
  - Extended Header (variable length)
  - Content (variable length)
  - Metadata (variable length)
- The _header_ section has the same format as version 2 protocol, and should contain the following information:
  - The header version (the first two bytes) will be incremented to '0x0002'
  - The Body size is the total byte size for the extended header, content, and Metadata. This will allow old clients to skip the entire message and read the sucessive message properly.
  - The other fields are filled in the same as the previous version.
- The _extended header_ section contains the following fields:
  - Extended header size (EXT_HEADER_SIZE) (2 bytes)
  - Metadata size (METADATA_SIZE) (2 bytes)
  - Message ID (MSG_ID) (4 bytes)
- The _content_ section is equivalent to the body section in the previous version.
  - The size of content can be computed as: BODY_SIZZE - (EXT_HEADER_SIZE + METADAT_SIZE)
- The _metadata_ section contains pairs of 'key' and 'value' strings. Keys are ASCII string, while values can be stored using different encodings.


Message Structure
=================

The OpenIGTLink protocol defines a set of message formats for several data types
that are frequently used for image-guided and robot-assisted interventions.
Those formats are used to compose messages that are transferred from one device
to another over the local area network. The application developers can choose
their own transportation layer that fits for their application and environment
(e.g. TCP, UDP, WebSocket).

While the developers are encouraged to use the data types defined in the
standard protocol, they have an option to define a new message format.
User-defined messages can be mixed with the standard message types, since the
protocol has a mechanism to skip a message, if the receiver does not know its
format. 

In OpenIGTLink Version 3, each OpenIGTLink message consists of the following
four sections:

~~~~
  Bytes
  0         58            72 
  +----------+-------------+-------------------+-----------+
  |  HEADER  | EXT_HEADER  |      CONTENT      | META_DATA | 
  +----------+-------------+-------------------+-----------+
             |<----------------- Body -------------------->|
~~~~

* Header (58 bytes)
* Extended Header (variable length) (New in Version 3)
* Content (variable length)
* Metadata (variable length) (New in Version 3)

The last three sections are called "Body" for the sake of convention. Since
there were no Extended Header and Metadata in the older versions before to 
Version 3, the Body section was solely used by the message content.
Therefore, the Body Size in the Header represented the size of the message 
content as well as the size of the rest of the message.
As a result, many old applications assume that the Body Size in the Header
equals the size of the message content. 

When the message structure was revised for Version 3, we redefined the Body
Size as the total size of Extended Header, Content, and Metadata, because
this new definition allows the old OpenIGTLink programs can still tell the
size of the rest of the message, and skip reading the byte stream until the
beginning of the next message. The size of the content can be computed as:
BODY_SIZE - (EXT_HEADER_SIZE + METADAT_SIZE).


Header + Extended Header
-------------------

~~~~
  Bytes
  0   2                       14                                      34
  +---+-----------------------+---------------------------------------+
  | V | TYPE                  | DEVICE_NAME                           | 
  +---+-----------------------+---------------------------------------+

  34              42              50              58
  +---------------+---------------+---------------+
  | TIME_STAMP    | BODY_SIZE     | CRC64         |
  +---------------+---------------+---------------+
  
  
  58                60              64        68         72    
  +-----------------+---------------+---------+-----------+
  | EXT_HEADER_SIZE | METADATA_SIZE | MSG_ID  | RESERVED  |
  +-----------------+---------------+---------+-----------+
~~~~

The formats of the Header and Extended Header sections are consistent among
all message types, and can be interpreted by any software that has an
OpenIGTLink interface. The Header contains device type (or data type) name,
which specifies the format of the body. The Extended Header section provides
a mechanism to attach application-specific meta-data to the message
along with the Metadata section.

Content
-------
The format of contenst section is type-dependent. Please see individual
type definition page linked below.

Meta-Data
---------
Meta-data are given in the form of an associative array (i.e. pairs of "key" and
"value") in the protocol. The Content section contains the data. The format of
the Content section is defined
for each data type.


Metadata header:

~~~~
  Bytes
  0             2             4                   6               10
  +-------------+-------------+-------------------+---------------+----
  | INDEX_COUNT | KEY_SIZE_0  | VALUE_ENCODING_0  | VALUE_SIZE_0  | ...
  +-------------+-------------+-------------------+---------------+----
                |<-------------- Metadata 0 --------------------->|


      10            12                  14              18	 
  ----+-------------+-------------------+---------------+----
  ... | KEY_SIZE_1  | VALUE_ENCODING_1  | VALUE_SIZE_1  | ...
  ----+-------------+-------------------+---------------+----
      |<--------------- Metadata 1 -------------------->|    
  
                                                  INDEX_COUNT*8+2
  ----+-------------+-------------------+---------------+
  ... |KEY_SIZE_N-1 |VALUE_ENCODING_N-1 |VALUE_SIZE_N-1 |
  ----+-------------+-------------------+---------------+
      |<----------Metadata N-1 (=INDEX_COUNT-1)-------->|
~~~~

Metadata body:

~~~~
  Bytes
  +--------+---------+--------+----------+----    ----+--------+-----------+
  | KEY_0  | VALUE_0 | KEY_1  | VALUE_1  |    ...     |KEY_N-1 | VALUE_N-1 |
  +--------+---------+--------+----------+----    ----+--------+-----------+
  |<-- Metadata 0 -->|<-- Metadata 1 --->|            |<-- Metadata N-1 -->|
~~~~

Please refer the following pages for the detailed format of the Header,
Extended Header, and Meta-Data sections.

* [Header](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/header.md)


Message Types
=============

Following types are supported.

Message types inherited from version 1
--------------------------------------

* [CAPABILITY](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/capability.md)
* [IMAGE](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/image.md)
* [POSITION](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/position.md) (alias of QTRANS)
* [QTRANS](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/qtransform.md) (formerly POSITION)
* [STATUS](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/status.md)
* [TRANSFORM](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/transform.md)

Message types introduced in version 2
-------------------------------------
* [BIND](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/bind.md)
* [COLORT](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/colortable.md)
* [IMGMETA](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/imagemeta.md)
* [LBMETA](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/labelmeta.md)
* [NDARRAY](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/ndarray.md)
* [POINT](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/point.md)
* [POLYDATA](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/polydata.md)
* [QTDATA](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/qtrackingdata.md)
* [SENSOR](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/sensordata.md)
* [STRING](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/string.md)
* [TDATA](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/trackingdata.md)
* [TRAJ](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/trajectory.md)

Message types introduced in version 3
-------------------------------------
* [COMMAND](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/command.md)


Query Mechanism
===============

See [Query Mechanism](https://github.com/openigtlink/OpenIGTLink/blob/master/Documents/Protocol/query.md) for detail.



