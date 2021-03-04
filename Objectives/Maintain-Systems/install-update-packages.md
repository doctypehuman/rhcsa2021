## Install Uptade Packages from Red Hat Network or Local Repository

RHEL uses *YUM* as a package manager. It is an acronym for Yellowdog Update Modifier. 
Yum installs packages from repositories that are stored in /etc/yum.repos.d/
In this directory you will find the repositories that are available.
If you want to have a look at the repositories that are available simply execute the command *yum repolist*
A repo file has the suffix .repo and you can create your own repo file. This file will basically contain the information 
required for YUM to look for the directory where all the packages are stored. The format of the repo file is as shown below 

	[test] #label name of the repo
	name= test #name of the repo
	baseurl= http://location.of.remote.repo.where.packages.are.stored. #location of the remote repository
	enabled= 1 # 1 is for enabled and 0 is for disabled
	gpgcheck= 1 #1 is for enabled and 0 is for disabled
	gpgkey= lcoation of gpg key


This the format of the file. Gpgcheck is a field which will tell the system if the repo has a gpgkey and if it needs to be checked. For repositories that are pulled from the internet this is a must. For local repositories this is not required. Below this field is the location of the gpg key. 

Amongst all the fields in the repo file, the most important field is the baseurl one. If the repository is hosted on your system the adress will begin with *file:///* . If it is hosted lcoally on intranet or on the internet the address will begin with *http://* or *https://* Notice the extra */* if the repo is hosted on your system. 

A sample repo file for BaseOS.repo which is hosted on my system in the folder "/repo" is given below for your reference. 

	[BaseOS]
	name= BaseOS
	baseurl= file:///repo/BaseOS/
	gpgcheck= 0


### Using YUM 

Here are some basic options that can be applied while using YUM.

- search  : Searches for packages in the repository
- search all 'package name'  : Searches all possible combinations for 'package name' is available repositories.
- provides \*/name-of-package : Deep search for files within the package
- install  : installs the package
- remove  : removes the package
- history : shows the history of downloads
- list : lists all packages 
- list installed  : lists installed packages
- group list : lists groups available
- group info  : list info of group
- undo : used after running history command, alternate way to remove packages
- group install : installs the group
- clean all : removes metadata of packages
- update  : updates the packages



