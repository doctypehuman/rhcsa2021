#Hard and Soft Links 

Linking is a usefule way to increase the accessibility of data wihout creating too many copies of the same. 
There are some basic differences that one must keep in mind between hard and soft links.


1. You cannot use hard links to link to directories. You can do this with soft links. 

2. Hard links which point to a file have to be on the same file system or on the same storage device.
   Soft links can point to a file which is located on another file system or storage device.


## Creating hard links 

The format is similar to *cp*

	ln file hard_link_to_file



## Creating Soft links 

	ln -s file soft_link_to_file


If a new name is not specified then the file or the directories name will be used. 



