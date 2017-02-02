---
layout: page
title: For Users
group: navigation
order: 2
description: ""
---
{% include JB/setup %}

OpenIGTLink is a network communication interface that allows real-time data
sharing among computers and devices connected to the local area network in the
procedure room. This page lists application software packages that come with the
OpenIGTLink interface. [The Tutorial page](/tutorials/) offers links to on-line
tutorials, where you can learn how to use OpenIGTLink in different software packages.

--------------------------------------------------------------------------------

Research Software Packages
==========================

3D Slicer
---------

> Web page: [http://www.slicer.org](http://www.slicer.org)

Slicer, or 3D Slicer, is a free, open source software package for visualization and image analysis. 3D Slicer is natively designed to be available on multiple platforms, including Windows, Linux and Mac Os X. 3D Slicer 3.x and 4.x come with an OpenIGTLink interface module that allows exchanging various data with external software and devices. See [documentation for OpenIGTLink IF module for 3D Slicer 4.6](https://www.slicer.org/wiki/Documentation/4.6/Modules/OpenIGTLinkIF).


Plus (Public software Library for UltraSound imaging research) 
--------------------------------------------------------------

> Web page: [http://www.plustoolkit.org](http://www.plustoolkit.org)

Plus is a software package containing library functions and applications for tracked ultrasound image acquisition, calibration, and processing. Features include:

* B-mode and RF acquisition using a wide range of imaging and tracking devices
* Live image and tracking data transfer to 3D Slicer using OpenIGTLink
* Spatial and temporal calibration
* Volume reconstruction

Plus has an OpenIGTLink interface that allow you to import those data into other OpenIGTLink-compatible software such as 3D Slicer.

Development of the Plus library is supported by Cancer Care Ontario by funding an Applied Cancer Research Unit at [the Laboratory for Percutaneous Surgery (PerkLab) at Queen's University](http://perk.cs.queensu.ca).


IGSTK (The Image-Guided Surgery Toolkit)
----------------------------------------

> Web page: [http://www.igstk.org](http://www.igstk.org)

The Image-Guided Surgery Toolkit is a high-level, component-based framework which provides a common functionality for image-guided surgery applications. The framework is a set of high-level components integrated with low-level open source software libraries and application programming interfaces (API) from hardware vendors.

The cornerstone of IGSTK is robustness. IGSTK provides the following high-level functionality: the ability to read and display medical images, including CT and MRI in DICOM format; an interface to common tracking hardware (e.g., AURORA from NDI); GUI and visualization capabilities, including four-quadrant view (axial, sagittal, coronal, and 3D) and multi-slice axial view (from 1 x 1 to many by many, such as 10 x 10); point-based registration and a means for selecting these points; and robust common internal software services for logging, exception-handling and problem resolution.

IGSTK has an OpenIGTLink interface providing connectivity with other OpenIGTLink-compatible software. See [IGSTK Book](http://igstk.org/IGSTK/img/IGSTKTheBookV2.pdf) for more detail.

CustusX
-------

> Web page: [http://custusx.org/](http://custusx.org/)

CustusX is a Navigation System for Image-Guided Intervention developed by the team of clinicians and engineers at the Norwegian National Competence Centre for Ultrasound and Image-Guided Therapy. From its start fifteen years ago, CustusX has been used in different clinical areas like neuro-, laparoscopic- and vascular surgery, interventional radiology and bronchoscopy. The navigation system has been designed to merge and visualise information from multiple medical imaging modalities, but with a focus on ultrasound and intra-procedure imaging.

IBIS
----

> Web page: [http://ibisneuronav.org/](http://ibisneuronav.org/)

The Intraoperative Brain Imaging System (Ibis) is an open source image-guided neurosurgery (IGNS) platform that replicates most of the basic functionality of it commercial counterparts while allowing for rapid development of new techniques. The platform focuses on intraoperative imaging such as tracked ultrasound and improved visualization throught the use of augmented reality.

Ibis was originally developed by Simon Drouin and Anka Kochanowska in the NeuroImaging and Surgical Technologies lab at the Montreal Neurological Institute.

Echelon
-------

> Web page: [http://www.imaging.robarts.ca/petergrp/Technology](http://www.imaging.robarts.ca/petergrp/Technology)

Echelon is an image guidance platform based on the Atamai Viewer, specifically designed specifically for real-time intracardiac IGS. A paired-down version of Echelon is licensed to NeoChord (under the name ‘NeoNav’) for use in their image guidance system.


MITK-IGT
--------

> Web page: [http://mitk.org/wiki/IGT](http://mitk.org/wiki/IGT)

The Medical Imaging Interaction Toolkit (MITK) is a free open-source software system for development of interactive medical image processing software. MITK combines the Insight Toolkit (ITK) and the Visualization Toolkit (VTK) with an application framework. As a toolkit, MITK offers those features that are relevant for the development of interactive medical imaging software covered neither by ITK nor VTK, see the Toolkit Features for details.


BioImage Suite
--------------

> Web page: [http://bioimagesuite.yale.edu/](http://bioimagesuite.yale.edu/)

BioImage Suite is an integrated image analysis software suite developed at Yale University. BioImage Suite has been extensively used at different labs at Yale since about 2001.


NifTK
-----

> Web page: [http://www.niftk.org/](http://www.niftk.org/)

NifTK is the name of our platform, combining NiftyReg, NiftySim, NiftyRec and NiftySeg via the viewer NiftyView developed by Translational Imaging Group at University Colledge London. The group has released a network communication library named [NiftyLink](http://cmic.cs.ucl.ac.uk/NiftyLink-API/), which uses OpenIGTLink for network data transfer.











