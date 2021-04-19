# List Create Delete Partitions MBR and GPT 

To use a hard disk it needs to be have partitions. MBR and GPT offer two methods of creating partitions. 




## MBR aka Master Boot Record 

The initial method of creating partitions. Since it's inception computers and hard disks have come a long way in terms of capacity of storage. While MBR did solve the inital issues, in it's current state it has some limitations. Partition size data is stored in 32 bit values so in effect it can have only 4 partitions. 3 primary and 1 logical. With the help of the logical partition we could in the end have 15 partitions on the disk. Let's us have a look at how to manage partitions using MBR.

In order to manage partitions on MBR the facility *fdsik* is used. For example if we have a disk /dev/sdb. Now on this disk we will create , list , delete and write partitions. 

- List current partitions 

The first step is to activate the disk using fdisk.

		fdisk /dev/sdb

Using this we enter the disk. To list current partitions simply type *p*

List of current partitions will be displayed. 

- Create a partition

To create a partitions you need to type *n*

By default the partition that is made is of Linux FileSystem ( 83 ) to change it to LVM or SWAP use the relevant codes.

- List File System Type

While creating a partition , file system type must be assigned to it. For MBR below are the most relevant types for LINUX

83 -> Linux File System

82 -> SWAP 

8e -> LVM 

- Writing Changes

Type *w* to write the changes to the disk. 

Once the changes are written you will exit the facility and then to reconfirm the changes it's best to type *partprobe*


- Edit Partitions

To edit existing partitions in MBR once you are in the disk, type *t*

- Delete Partitions

To delete an existing partition in MBR type *d* to delete. 




### GPT aka Guided Partition Table

To overcome the shortcomings of MBR ( limited partitions, limited size ) GPT was introduced. Instead of using 32 bit values to store data, it uses 128 bit values. 
With this the number of partitions that are possible increases to 128 and the maximum data that can be stored increases to 8 Zebibyte which is 1024 X 1024 X 1024 X 1024 gigabytes.

In order to manage partitions on GPT the facility *gdisk* is used. For example if we have an unused disk /dev/sdc we can use gdisk /dev/sdc to manage partitions on it.


All options that are used for MBR in fdisk utility are the same fin gdisk for GPT. 



