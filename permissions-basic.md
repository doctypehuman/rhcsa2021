# Permissions - Basic


Everything is a file in Linux and each file has a set of permissions associated with it. Who can access it , who can change it and who can execute it. Along with files, directories also have permissions. In this chapter we will be discussing the basic permissions associated with files and directories. 

There are three basic permissions. *Read* , *Write* and *Execute* . These are further grouped for *User*, *Group* and *Other*

#### Interpreting File Permissions 

Use the option *-l* to view the detailed listing of a directory. Limited sample of the output is as below 

	drwxr-xr-x. 1 user group 0 Feb 8 17:30 example

This is the ouput for a directory. The "d" in the begining is the sign for it. If it were a file the output would be something like this 

	-rwxr-xr-x. 1 user group 0 Feb 8 17:30 example


Right, so we now know how to differentiate between folders and file. Let's further break down the aplhabets after the "d".
User, Group and Others are grouped together with their permissions. In the above example the first three letters after the "d" refer to the permissions for the user. The next three for the group and the last three for others. "-" signifies that no permission. Hence in the above example _Others_ have only *read* and *execute* permissions for the file. 

Let us now examine what these permissions mean for a file and for a directory. 

1. Files 

- Read (r) : Contents of the file can be read.
- Write (w) : Contents of the file can be changed.
- Execute (x) : File can be executed as a command.

2. Directory

- Read (r) : Contents of the directory can be listed.
- Write (w) :Any file can be created or deleted from the directory.
- Execute (x) :Contents of the directory can be accessed.( Dependant on the permission of the files in the directory)

This bit is slightly important because if a directory is given only Read permissions then the contents will only be listed but cant be accessed. If the directory is given only Execute as a permission then the contents of the directory cannot be listed.  Generally a directory is given *r-x* permission. That means that you can list and access the files in the directory but cannot create or delete files in it. 


#### Representing permissions 

Permissions when displayed are always represented with letters ( r - w - x ) but when they are being set they can be represented using letters or numbers. 

1. Representing permissions with letters

User -> u
Group -> g 
Other -> o
All -> a

Read -> r
Write -> w
Execute -> x

\+ -> add a permission
\- -> remove a permission
\= -> set a permission ( to replace the entire set for a group of permission)

The command to set permissions is *chmod* An example 

	chmod a+x test-script.sh

The above example will make the file test-script.sh executable for all. 

The same result can be achieved by using numeric values as well. Once you get a hang of that it will be much easier .

2. Representing permissions with numbers.

4 = Read
2 = Write 
1 = Execute

The total of this is 7 and it is used for User, Group and Other. So if a file has to be given read,write and execute permissions only for the user and no permission for anyone else , the permission will be represented as 700. If the same file want to add read and execute permissions for group and others as well, the permission will be represented as 755.

	chmod 755 script.sh


