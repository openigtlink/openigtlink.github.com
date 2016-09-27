---
layout: page
title: Specification > Video
header: Pages
---
{% include JB/setup %}


## Summary

The Video format supports video codec streaming with metric information including codec protocal name,
frame height, frame width, time interval. The body section of the VIDEO
data consists of two parts: video header to transfer the metric information and video body
to transfer encoded video bit stream. The numerical values can be 8-, 16-, 32-bit integer, depending on the encoder.
The pixel values can be either big-endian or little-endian. This message type could be used for real-time video transmission. 
A demonstration program could be found here: [VideoStreamingOpenIGTLink](https://github.com/openigtlink/VideoStreamingOpenIGTLink)



## Message Types
### Video bit stream

<table border="1" cellpadding="5" cellspacing="0" align="center">
<tr>
<td style="background:#e0e0e0;"> Data
</td><td style="background:#e0e0e0;"> Type
</td><td style="background:#e0e0e0;"> Description
</td></tr>
<tr>
<td align="left"> V
</td><td align="left"> unsigned short
</td><td align="left"> version number
</td></tr>
<tr>
<td align="left"> T
</td><td align="left"> 8bit unsigned int
</td><td align="left"> Number of video bit stream Components (1:Scalar, &gt;1:Vector). (NOTE: Vector data is stored fully interleaved.)
</td></tr>
<tr>
<td align="left"> S
</td><td align="left"> 8bit unsigned int
</td><td align="left"> Scalar type (2:int8 3:uint8 4:int16 5:uint16 6:int32 7:uint32)
</td></tr>
<tr>
<td align="left"> E
</td><td align="left"> 8bit unsigned int
</td><td align="left"> Endian for video bit stream data (1:BIG 2:LITTLE) (NOTE: values in video header is fixed to BIG endian)
</td></tr>
<tr>
<td align="left"> VIDEO_DATA
</td><td align="left"> Binary video bit stream data ()
</td><td align="left"> bit stream data  (endian is determined by "E" field)
</td></tr>
</table>

### STT_VIDEO

<table border="1" cellpadding="5" cellspacing="0" align="center">
<tr>
<td style="background:#e0e0e0;"> Data
</td><td style="background:#e0e0e0;"> Type
</td><td style="background:#e0e0e0;"> Description
</td></tr>
</table>

### STP_VIDEO

<table border="1" cellpadding="5" cellspacing="0" align="center">
<tr>
<td style="background:#e0e0e0;"> Data
</td><td style="background:#e0e0e0;"> Type
</td><td style="background:#e0e0e0;"> Description
</td></tr>
</table>
## Notes

The vector type is just reserved for future development.

## Implementations

Video message type is implemented in the following files:

* [igtlVideoMessage.h](https://github.com/openigtlink/OpenIGTLink/blob/master/Source/igtlVideoMessage.h)
* [igtlVideoMessage.cxx](https://github.com/openigtlink/OpenIGTLink/blob/master/Source/igtlVideoMessage.cxx)

## Contributors
* Longquan Chen, Junichi Tokuda
