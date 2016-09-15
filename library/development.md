---
layout: page
title: SDK > Development 
description: ""
---

## Development of OpenIGTLink C/C++ Library

The OpenIGTLink C/C++ Library is being developed by the open-source community. This papge describes the detail of its development process.

### Repository

We use [GitHub](https://github.com/openigtlink/OpenIGTLink) as a primary repository for the library. The source code is managed at [GitHub](https://github.com/openigtlink/OpenIGTLink). You are welcome to [fork](https://help.github.com/articles/fork-a-repo/) the repository to your personal repository, and modify it for your own project. If you have fixed existing bug or made some improvement, you are encouraged to contribute them to the main repository by submitting a pull request.

### Coding Style

We follow [the ITK Style Guide](http://www.vtk.org/Wiki/images/c/c6/ITKStyle.pdf) to keep the coding style consistent, and improve the readability of the code. If you wish to contribute your code to ITK, please make sure that your code follows this style guide.

### Buliding

The OpenIGTLink C/C++ Library uses [CMake](https://cmake.org/) to manage the cross-platform development. CMake reads platform-independent configuration files in the source directory and generates bulid files (e.g. makefiles for Linux, Mac OX X, and UNIX operating systems, and projects/workspaces for Microsoft Visual C++ environment), which are then processed by the native compilers to build binaries. 

### Quality Assuarance

Several quality assurance processes are implemented at different development stages:

* New [messaging protocols](../spec.html) are always designed and reviewed transparently by the community, before being released. The backward compatibility is always out priority.
* The [_Fork & Pull Model_](http://stackoverflow.com/questions/11582995/what-is-the-fork-pull-model-in-github) is used to ensure that all codes contributed to the repository are tested before being merged. This also makes it easier to track contributions from individual developers.
* Bugs and issues are tracked at [GitHub Issue Tracker](https://github.com/openigtlink/OpenIGTLink/issues).
* [CTest](https://cmake.org/Wiki/CMake/Testing_With_CTest) is used to test the function of the library. Currently, only the underlying C library is tested using CTest.
* The library is used in popular software packages, such as [3D Slicer](https://www.slicer.org/) and [PLUS](https://www.assembla.com/spaces/plus/wiki). Those software packages are tested daily, and reported to [3D Slicer Dashboard](http://slicer.cdash.org/index.php?project=Slicer4) and [PLUS Dashboard](http://crunch.cs.queensu.ca/CDash/index.php?project=PLUS).
* We are using [Travis CI](https://travis-ci.org/) (for Mac/Linux) and [AppVeyor](https://ci.appveyor.com/project/openigtlink/openigtlink) (for Windows) as a primary [continuous integration (CI)](https://en.wikipedia.org/wiki/Continuous_integration) platform. Travis CI and AppVeyor pull the code from the repository at GitHub, bulid the code, and post the results in [the SDK page](../sdk). GitHub triggers this testing process whenever the repository is updated. Travis CI is currently supporting Linux and Mac OS X. Windows suupport has been [discussed](https://github.com/travis-ci/travis-ci/issues/2104), and may become available in the future.

### Related Links
* [OpenIGTLink C/C++ Library Repository](https://github.com/openigtlink/OpenIGTLink)






