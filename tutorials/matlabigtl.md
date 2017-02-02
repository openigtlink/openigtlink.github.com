---
layout: page
title: Tutorials > Matlab/OpenIGTLink
header: Pages
---
{% include JB/setup %}

##Before You Start...
There are currently two implementations of OpenIGTLink interfaces for Matlab:
1. Matlab/OpenIGTLink interface developed in 2008 (see below)
2. [New Matlab Interface](https://www.assembla.com/spaces/plus/wiki/Matlab_interface) developed by [Perk Lab. at Queen's University](http://perk.cs.queensu.ca)

Since we released the Matlab/OpenIGTLink interface in 2008, we have learned that some users had troubles building Matlab MEX files due to incompatibility between Matlab and C++ compilers installed in their systems. To address this issue, the team at Queen's University developed the new Matlab Interface that does not require MEX. We recommend to check [their page](https://www.assembla.com/spaces/plus/wiki/Matlab_interface), before deciding which to use.


##About Matlab/OpenIGTLink
The objective of this project is to provide OpenIGTLink interface for [Matlab](http://www.mathworks.com/) / [Octave](http://www.gnu.org/software/octave/) to support research and development in image guided therapy (IGT). Matlab and Octave are widely used for prototyping image and signal processing algorithms. They also offer many powerful function sets to handle matrix and coordinate data, which is useful to test and analyze coordinate data exported from tracking and robotic devices.

The OpenIGTLink interface for Matlab / Octave allows importing and exporting several types of data that can be handled in the OpenIGTLink protocol in a Matlab / Octave environment. It provides a rapid prototyping environment, which many researchers and engineers are already familiar with.

The Matlab/OpenIGTLink is an alternative solution to [Slicer Matlab Pipeline Project](http://www.na-mic.org/Wiki/index.php/Projects/Slicer3/2007_Project_Week_Slicer_Matlab_Pipeline_for_scalars_and_tensors) in 2007 NA-MIC Project Week.

##Demo Videos
###Scenario 1: Push image data to 3D Slicer from Matlab console (1-way communication)
Matlab and 3D Slicer are running on different hosts (the Matlab window is displayed using remote display). A matrix 'I' and 'M' on the Matlab console contain image data and affine transformation respectively. With just a several lines of commands on the Matlab console, the image data is transferred to the 3D Slicer through the network using OpenIGTLink. 

[Demo Video: Scenario 1](http://www.na-mic.org/Wiki/images/5/53/OpenIGTLink_Matlab_1way.mov)


###Scenario 2: Request Matlab to process image data from 3D Slicer (2-way communication)
Matlab and 3D Slicer are running on different hosts (Matlab window is displayed using remote display). On the Matlab console, an example image processing server ('example_server.m') is running. This example server basically receives an image form external software, apply a filter and return a result. Once the OpenIGTLink connection between the 3D Slicer and the Matlab is established, the example MR image is loaded into the scene on the 3D Slicer, and then pushed to the Matlab through the OpenIGTLink connection. After a few seconds, the Matlab returns the filtered image to the 3D Slicer through the same OpenIGTLink connection. The image is visualized on the 3D Slicer.

[Demo Video: Scenario 2](http://www.na-mic.org/Wiki/images/1/1c/OpenIGTLink_Matlab_2way.mov)

### Scenario 3: Send transform (4x4 matrix) from Matlab to 3D Slicer
Matlab and 3D Slicer are running on different hosts (Matlab window is displayed using remote display). The video demonstrates to manipulate 4x4 matrix on the Matlab console and then transfer to the 3D Slicer through the network using OpenIGTLink.


[Demo Video: Scenario 3](http://www.na-mic.org/Wiki/images/0/08/OpenIGTLink_Matlab_tracking.mov)

## How does it work?
The OpenIGTLink Matlab interface is implemented as a set of MEX Files, which are C/C++ source codes called from Matlab. Those MEX files simply receive data from Matlab, connect to the OpenIGTLink receiver, serialize the data in an appropriate format using the OpenIGTLink Library, and send it to the receiver.

The usage of the interface is quite simple. The following example Matlab code is sending trancking data to the receiver waiting at port #18944 on the localhost.

    %%% affine transform matrix
    M = [1.0, 0.0, 0.0, 0.0;
         0.0,-1.0, 0.0, 0.0;
         0.0, 0.0, 1.0, 0.0;
         0.0, 0.0, 0.0, 1.0];
    
    IMGDATA.Type = 'TRANSFORM';
    IMGDATA.Name = 'MatlabTrans';
    IMGDATA.Trans = M;
    
    sd = igtlopen('localhost', 18944);
    r = igtlsend(sd, IMGDATA);
    igtlclose(sd);


For tracking data transfer:

    %%% read image data
    fid = fopen('igtlTestImage1.raw', 'r');
    I = fread(fid, [256 256], 'uint8')';
    fclose(fid);
    
    %%% affine transform matrix
    M = [1.0, 0.0, 0.0, 0.0;
         0.0,-1.0, 0.0, 0.0;
         0.0, 0.0, 1.0, 0.0;
         0.0, 0.0, 0.0, 1.0];
    
    IMGDATA.Type = 'IMAGE';
    IMGDATA.Name = 'MatlabImage';
    IMGDATA.Image = I;
    IMGDATA.Trans = M;
    
    %%% send the image data through OpenIGTLink connection
    sd = igtlopen('localhost', 18944);
    r = igtlsend(sd, IMGDATA);
    igtlclose(sd);


## Download & Building OpenIGTLink Mex functions

### For Windows Users
You may download mex binary files for 32-bit and 64-bit Windows built by Dr. Nicolas Herlambang, Ph.D. (Aze Ltd., Japan) from the following link.

* [OpenIGTLinkMex_Win32.zip](http://www.na-mic.org/Wiki/index.php/File:OpenIGTLinkMex_Win32.zip) (32 bit).
* [OpenIGTLinkMex_Win64.zip](http://www.na-mic.org/Wiki/index.php/File:OpenIGTLinkMex_Win64.zip) (64 bit).

### For Linux Users
* [OpenIGTLinkMex_Linux64.tar.gz](http://www.na-mic.org/Wiki/index.php/File:OpenIGTLinkMex_Linux64.tar.gz) (64 bit -- Built on 64-bit FC13 + Matlab 7.10.0 R2010a)

#### Install the OpenIGTLink Library
The instruction can be found in the [SDK Page](/library.html). We recommend to build the library as a static library. (Just to avoid a trouble that Matlab couldn't find shared objects/dynamic link library. In principle, either static or shared library works.)

#### Get the Matlab OpenIGTLink interface source code
The OpenIGTLink/Matlab interface is in the initial stage of development. The source code is available from NA-MIC SandBox repository at [NA-MIC SandBox Subversion Repository](http://svn.na-mic.org/NAMICSandBox/trunk/MatlabIGTL).

#### Build MEX files
CMake configuration (CMakeLists.txt) comes with Matlab OpenIGTLink interface. To build the interface with CMake
in Linux/Mac OS X environment,

    cd <working directory>
    svn co URL: http://svn.na-mic.org/NAMICSandBox/trunk/MatlabIGTL
    mkdir MatlabIGTL-build
    cd MatlabIGTL-build
    ccmake ../MatlabIGTL

This will launch Curses Interface for CMake. Press 'c' to configure and check the following parameters;
* MEX_COMPILER = (path to Matlab's ''mex'' command or Octave's ''mkoctfile'')
* OpenIGTLInk_DIR = (path to binary directory of OpenIGTLink)

Then press 'g' to generate a makefile. Press 'q' to quit the CMake interface screen.
Once you find '''Makefile''' in the directory, run make. Several files with extension \*.mex (or \*.mex &lt;arc-name&gt;) will be generated.

## Contact
If you have any question, please subscribe to OpenIGTLink ML.
You may also contact to [Junichi Tokuda](http://www.spl.harvard.edu/pages/People/tokuda) for further information.
