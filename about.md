---
layout: page
title: About
group: navigation
order: 1
---
{% include JB/setup %}

OpenIGTLink is an open-source network communication interface specifically
designed for image-guided interventions. It aims to provide a plug-and-play
unified real-time communications (URTC) in operating rooms (ORs) for image-guided
interventions, where imagers, sensors, surgical robots,and computers from
different vendors work cooperatively. This URTC will ensure the seamless data
flow among those components and enable a closed-loop process of planning, control,
delivery, and feedback. Examples applications of URTC include but not limited to:

- Stereotactic surgical guidance using optical position sensor and medical image visualization software
- Intraoperative image guidance using real-time MRI and medical image visualization software
- Robot-assisted interventions using robotic devices and surgical planning software

The [specification of OpenIGTLink](spec) is open, and can be used without any license fee;
hence OpenIGTLink is suitable for both industrial and academic developers. We also provide
a reference implementation of the protocol as a [C/C++ library](sdk).


License
=======

[The specification of the OpenIGTLink protocol](spec) and [it's reference C/C++ implementation](https://github.com/openigtlink/OpenIGTLink.git) are both provided to the public under [the new BSD License](http://www.opensource.org/licenses/BSD-3-Clause). Unlike some other open-source licenses, it does not require that source code be distributed at all.


Acknowledgement
===============

The OpenIGTLink project is primarily supported by the U.S. National Institutes of Health (NIH R01EB020667, PI: Junichi Tokuda).
There are also several research projects that are supporting the development of OpenIGTLink including:

* [NIH R01EB020667: OpenIGTLink: a network communication interface for closed-loop image-guided interventions](http://projectreporter.nih.gov/project_info_details.cfm?aid=8944250&icde=25344808&ddparam=&ddvalue=&ddsub=&cr=1&csb=default&cs=ASC) (PI: Junichi Tokuda)
* [NIH R01CA111288: Enabling Technologies for MRI-Guided Prostate Interventions](http://www.ncigt.org/pages/Collaborations/Enabling_Technologies_for_MRI-Guided_Prostate_Interventions_R01-CA111288) (PI: Clare M. Tempany)
* [NIH P41EB015898: National Center for Image-Guided Therapy (NCIGT)](http://www.ncigt.org/) (PI: Ferenc A. Jolesz / Clare M. Tempany)
* NIH 5R01CA138586: A New Method for Improved Targeting in Image-Guided Abdominal Interventions (PI: Nobuhiko Hata)
* [National Alliance for Medical Image Computing (NA-MIC)](http://www.na-mic.org/) (PI: Ron Kikinis)
* Intelligent Surgical Instrument Project sponsored by The Ministry of International Trade and Industry, Japan (PI: Makoto Hashizume)

Contributors
============

* [Junichi Tokuda, Ph.D.](http://www.spl.harvard.edu/pages/People/tokuda), Brigham and Women's Hospital (Lead Developer)
* [Nobuhiko Hata, Ph.D.](http://www.spl.harvard.edu/pages/People/noby), Brigham and Women's Hospital
* [Clare M. Tempany, M.D.](http://www.spl.harvard.edu/pages/People/ctempany), Brigham and Women's Hospital
* [Kiyoyuki Chinzei, Ph.D.](http://staff.aist.go.jp/k.chinzei/), National Institute of Advanced Industrial Science and Technology, Japan
* [Ron Kikinis, M.D.](http://www.spl.harvard.edu/pages/People/kikinis), Brigham and Women's Hospital
* [Ferenc Jolesz, M.D.](http://www.spl.harvard.edu/pages/People/jolesz), Brigham and Women's Hospital
* [Tina Kapur, Ph.D.](http://www.spl.harvard.edu/pages/People/tkapur), Brigham and Women's Hospital
* [Steve Pieper, Ph.D.](http://www.spl.harvard.edu/pages/People/pieper), Isomics, Inc.
* [Isaiah Norton](http://golbylab.bwh.harvard.edu/people/nortonIsaiah.html), Brigham and Women's Hospital
* [Gabor Fichtinger, Ph.D.](http://research.cs.queensu.ca/~gabor/), Queen's University, Canada
* [Tamas Ungi, M.D., Ph.D.](http://perk.cs.queensu.ca/profiles/ungi), Queen's University, Canada
* [Andras Lasso, Ph.D.](http://perk.cs.queensu.ca/profiles/lasso), Queen's University, Canada
* [Gregory S. Fischer, Ph.D.](http://aimlab.wpi.edu/people/Gregory_Fischer), Worcester Polytechnic Institute
* [Matt Clarkson, Ph.D.](http://cmic.cs.ucl.ac.uk/), Centre For Medical Image Computing, University College London, UK.
* [Adam Rakin](http://www.imaging.robarts.ca/petergrp/node/113), Unniversity of Western Ontario / Roberts Research Institute, Canada
* [Sebastian Tauscher, M.Sc.](http://www.imes.uni-hannover.de/11.html?&L=1&tx_tkinstpersonen_pi1%5Balias%5D=tauscher&cHash=87be8789251f292d9707429a8782d013), Institut f&uuml;r Mechatronische Systeme, Leibniz Universit&auml;t Hannover
* [Laurent Chauvin, M.S.](http://www.spl.harvard.edu/pages/People/lchauvin), Brigham and Women's Hospital
* [Luis Ib&aacute;&ntilde;ez, Ph.D.](http://www.kitware.com/profile/team/ibanez.html), Kitware, Inc.
* Patrick Cheng, Ph.D., Georgetown University
* [Peter Kazanzides, Ph.D.](http://eng.jhu.edu/wse/systems-institute/page/peter-kazanzides), Johns Hopkins University
* [Jumpei Arata, Ph.D.](http://arata.web.nitech.ac.jp/index.html), Nagoya Institute of Technology, Japan
* [Alex Golby, M.D.](http://golbylab.bwh.harvard.edu/people/golbyAlexandra.html), Brigham and Women's Hospital
* Andre Charles Legendre
* [Iulian I. Iordachita](https://www.lcsr.jhu.edu/User:Iiordachita/CV), Johns Hopkins University
* [Jan Egger, Ph.D., Ph.D](http://www.spl.harvard.edu/pages/People/egger), Brigham and Women's Hospital
* [Haying Liu](http://www.spl.harvard.edu/pages/People/hliu), Brigham and Women's Hospital
* [Yuichiro Hayashi](http://www.spl.harvard.edu/pages/People/yhayashi), Ph.D., Nagoya University, Japan
* [Atsushi Yamada, Ph.D.](http://www.spl.harvard.edu/pages/People/ayamada), Shiga University of Medical Science, Japan

### Institutes, Organizations
* [National Center for Image Guided Therapy](http://ncigt.org)
* [National Alliance for Medical Image Computing](http://na-mic.org)
* [Surgical Navigation and Robotics Laboratory, Brigham and Women's Hospital](http://snr.spl.harvard.edu)
* [Surgical Planning Laboratory, Brigham and Women's Hospital](http://www.spl.harvard.edu)
* [Automation and Interventional Medicine (AIM) Robotics Laboratory, Worcester Polytechnic Institute](http://aimlab.wpi.edu)
* [Laboratory for Percutaneous Surgery, Queen's University, Canada](http://perk.cs.queensu.ca)
* [Insight Software Consortium](http://www.insightsoftwareconsortium.org/)
* [Computer-Integrated Surgical Systems and Technology, Johns Hopkins University](http://www.cisst.org/)
* [Robotics and Automation Laboratory, Nagoya Institute of Technology, Japan](http://ral.web.nitech.ac.jp/members.html)

### Publications
1. Tokuda J, Fischer GS, Papademetris X, Yaniv Z, Ibanez L, Cheng P, Liu H, Blevins J, Arata J, Golby AJ, Kapur T, Pieper S, Burdette EC, Fichtinger G, Tempany CM, Hata N. [OpenIGTLink: an open network protocol for image-guided therapy environment](http://www.spl.harvard.edu/publications/item/view/1709). [Int J Med Robot](http://www3.interscience.wiley.com/journal/112094293/home). 2009 Dec;5(4):423-34.
1. Arata J, Kozuka H, Kim HW, Takesue N, Vladimirov B, Sakaguchi M, Tokuda J, Hata N, Chinzei K, Fujimoto H. Open core control software for surgical robots. Int J Comput Assist Radiol Surg. 2010 May;5(3):211-20.
1. Tokuda J, Fischer GS, DiMaio SP, Gobbi DG, Csoma C, Mewes PW, Fichtinger G, Tempany CM, Hata N. Integrated navigation and control software system for MRI-guided robotic prostate interventions. Comput Med Imaging Graph. 2010 Jan;34(1):3-8.
1. Elhawary H, Liu H, Patel P, Norton I, Rigolo L, Papademetris X, Hata N, Golby AJ. Intraoperative real-time querying of white matter tracts during frameless stereotactic neuronavigation. Neurosurgery. 2011 Feb;68(2):506-16.
1. Egger J, Tokuda J, Chauvin L, Freisleben B, Nimsky C, Kapur T, Wells W. Integration of the OpenIGTLink Network Protocol for image-guided therapy with the medical platform MeVisLab, Int J Med Robot. 2012 Sep;8(3):282-90. 
1. Tauscher S, Tokuda J, Schreiber G, Neff T, Hata N, Ortmaier T. OpenIGTLink interface for state control and visualisation of a robot for image-guided therapy systems. Int J Comput Assist Radiol Surg. 2014 Jun 13. 


