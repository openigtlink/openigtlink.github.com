---
layout: page
title: How to Contribute
description: ""
---

The OpenIGTLink Library is open-source software, and we always welcome your feedbacks, feature requests, and patches. There are several ways to contribute to the project. 

## Report bugs

### Create an issue in the issue tracker.

Log in Github with your account and open [OpenIGTLink repository page](http://github.com/openigtlink/OpenIGTLink.git). Then, click "Issues" and create "New Issue." Please briefly explain what kind of issue you are going to address, and how to reproduce the issue. 


## Contribute patches

We apply [GitHub Flow](https://guides.github.com/introduction/flow/) to our development process. Please follow the steps below to contribute your patch.


### Fork the library
In [the OpenIGTLink repository page](http://github.com/openigtlink/OpenIGTLink.git), click "Fork" on the right-left corner of the page, and choose your repository as a destination.


### Setup your local repository

You can clone the OpenIGTLink repository into your local directory using a git command. The OpenIGTLink Library comes with a shell script that configure your Git repository with valid author name, contact, and remote URLs. This shell script also sets up a pre-commit script to validate your source code before committing to the repository. These configurations are effective only within your local repository; the shell script needs to be executed every time a repository is cloned in your local disk.

First, clone the main OpenIGTLink repository:

    $ cd <working directory>
    $ git clone https://github.com/openigtlink/OpenIGTLink.git

This command will create a new folder "OpenIGTLink" under the \<working directory\>. From insdie the OpenIGTLink directory, run the configuration shell script:

    $ cd OpenIGTLink
    $ ./Utilities/SetupForDevelopment.sh 

The shell script will ask several questions about your author information, remote repository URLs, and Github account. This shell script will set up two remote URLs, namely 'github' and 'origin'. 'origin' is the main repository ( https://github.com/openigtlink/OpenIGTLink.git ), whereas 'github' is your fork ( https://github.com/\<your GitHub username\>/OpenIGTLink.git ).

### Modify the code

When you edit the code, please follow [VTK Coding Standards](http://www.vtk.org/Wiki/VTK_Coding_Standards). If you are planning to contribute your code, please make sure that the code can be compiled and linked without any error. The build instruction is available in [the Build Instruction page](build).

### Commit your change
To commit your change to your local repository:

    $ git commit -a -m "< summary of your change >"

When you commit your change, make sure to give a brief summary of your change as a comment. In the comment, you have to have:

* Type of your commit as a prefix in the comment txt. The prefixes are defined in [Commit Message Prefix](http://www.slicer.org/slicerWiki/index.php/Documentation/Nightly/Developers/Style_Guide#Commit_message_prefix) in [3D Slicer Project page](http://slicer.org/).
* Issue number (e.g. #15). Github will recognize the issue number and automatically refer your commit from the issue tracker, once you push your local repository to the forked repository in the Github server.

To push your local repository to your fork in GitHub,

    $ git push github master

You may use a branch other than 'master'. 

### Request "Pull"
From your forked repository, go to "Pull Request" and create "New pull request." Once you submit, the maintainer of the OpenIGTLink repository will be notified. The maintainer will review your commit, and either pull or reject it. Please note that we cannot guarantee that your changes are always merged into the main repository. 




