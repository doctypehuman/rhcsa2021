# Create Mount Unmount File Systems


Before you create a file system that can be mounted you need to prepare the device. Detailed instructions are mentioned in chapters pertaining to LVM.


Assuming that volume is prepared we can create a file system on it with `mkfs` command. To specify which type of file system you require use option `-t`.

To get a list of all available options for file systems press `tab` to use bash completion.


Below is a command where in we will create a ext4 file system on device /dev/sdb1


		mkfs -t ext4 /dev/sdb1


We have the file system ready but we need to mount it. We can mount it manually using the `mount` command or by making an entry in fstab file. 

Detailed instructions for fstab have already been mentioned so I would not be repeating it. When using the `mount` command it is essential to create a mount point.

While there is a generic mount point in the system in the form of `/mnt` you can create a custom point like so.


		mkdir /custom_mountpoint


We can now proceed to mount our newly created file system.


		mount /dev/sdb1 /custom_mountpoint


In order to umount the file system we need to use the `umount` command. We can either specify the mount point or the device that needs to be unmounted.


		umount /dev/sdb1

OR 


		umount /custom_mountpoint
