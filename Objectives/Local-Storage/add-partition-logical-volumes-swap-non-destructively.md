# Add Partitions Logical Volumes Swap Non Destructively

We will have a look at creating Logical Volumes and Swap File Systems here. For the logical volumes you must have already created the volume group with physical volumes assigned to it. For a Swap file system you need to create a partition with type Swap i.e code 82 for MBR and 8200 for GPT.


Let's have a look at SWAP first. SWAP is used primarily to help the kernel with memory should it get overloaded. When and if the kernel get overloaded it will offload some of it's memory pages to SWAP thereby creating some space for itself.

To see how much swap is currently available and how much is used type *free -h* 

As mentioned above, the first step in creating a SWAP file system is to create a partition with SWAP type. Once that is done it is a matter of few commands to get the filesystem up
and running.

Creating a swap filesystem is done like so 

		mkswap /dev/sd1

Once it is created, we need to activate it. That is done like so 

		swapon /dev/sd1

Now that it is activated we need to ensure that it is mounted automatically on boot. We do that by creating an entry in the fstab.

That's about it with swap. But wait, there more to it. What if we did not have free hard disks and we need to use swap since the kernel is getting overloaded.

In that case we can make a swap file. Creating a swap file is shown below for reference.

		

		dd if=/dev/zero of=/swapfile bs=1M count=100

		mkswap /swapfile

		swapon /swapfile

What the command dd if... does is that it generates 100 blocks of size 1Mib each to the /swapfile. That ways we will get a file of 100Mib to be used as a swapfile.


Alright, now that we have SWAP done, let's get to Logical Volumes. 



Logical Volumes represent the last step in Logical Volume Management. They are added to a Volume Group and they can be increased or decreased in size.
Please do bear in mind that XFS filesystems cannot be reduced. They can only be increased. Ext4 file systems can be decreased in size.

Creation of logical volumes is done like so

		lvcreate -n lvdata -L 10G vgdata

Here the option -n is for the name -L is the size followed by the size we wish to assign. In the end as an argument is the volume group from  which the logical volume will be created. When using logical extents to assign the size we need to use the option -l. Please note that we can use either -L or -l. We cannot use both of them at the same time.


To verify the creation of the logical volume we use the command *lvs* or *lvdisplay*

An important point to note is the nomenclature of the logical volume. The simplest way to remember is that it will always be /dev/volume_group/logical_volume.


We can now proceed to create a file system on the logical volume. 

		mkfs.xfs /dev/volumegroup/logicalvolume

Post that we need to mount it. We can either mount it manually using the *mount* command or we can create an entry in fstab. 


Resizing the logical volume is an important aspect that is very helpful. We use the command *lvresize* command for that. 

A simple example

		lvresize -r -L +1G /dev/volgroup/lvolume

In the above command we used the option -r so that the filesystem will also be included in the resizing. To specify the size we used -L followed by a plus sign to signify that we want to add 1G of space to it. In the end is the full path of the logical volume. In order to reduce you simply need to use the minus sign instead of the plus sign AND unmount the file system BEFORE reducing the size. Mount the file system once the reduction is done. Please note that for addition of space unmounting is not necessary.

Another point to consider is that before resizing the logical volume, should you be increasing the size, please ensure that the volume group to which it is attached has the required space on offer. 



