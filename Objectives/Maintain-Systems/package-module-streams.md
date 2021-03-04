# Working with package module streams

This is a specific feature available in RHEL8. In Application Stream Module different versions of packages can be found. Another advantage is that Application Module Stream allows to update certain critical packages more often. 

A module describes a set of packages that belong together. An example is container-tools. This module contains all the packages required for container management in RHEL8.
Typically modules are organised around a specific version of an application. In a module you will find all the dependancies of the application for that particular version.

Each module can have multiple application _streams._ A _stream_ contains a specific version and updates are provided for that specific version. When working with modules different streams are available but you can work with only one stream at a given time. 

Modules can also have different _profiles._ A _profile_ is a list of packages that are installed together for a particular purpose.You can come across different profiles such as minimal, server, default. When working with modules you can select a particualr profile. 


Think of a module like an ISO image file. The ISO version is the stream. The built ( minimal , server with GUI ) is the profile. 



### Finding Information on Modules


To look at the modules one needs to use Yum. 

	yum module list 

Will give the list of modules. In the output \[d\] is for default \[e\] is for enabled \[i\] is for installed \[x\] is for disbaled

	yum module info

Will give the information on the module

To find out more information on the availabe streams available for the particular module

	yum module list module-name


### Installing Modules


After finding out information on the module, it is time to download it. Every module has a default module stream providing access to a specific version. If that is the version that you need you can simply 

	yum module install module-name

But if there is a separate version that you need, then you need to first enable the module stream and then download it.

	yum module enable module:version-number

	yum module install module_name:version-number/profile


You can also switch versions. If you are currently on version x of python and want to switch to version y. 
You have to type

	yum install module python:y

After this, to ensure that all dependant packages that are not in the module are also updated run 

	yum distro-sync










 
