# Configure Compression 


Compression in RHEL is achieved by the Virtual Data Optimizer a.k.a VDO.  Tha main feature of VDO is data deduplication. On top of a VDO device either a file system can be mounted or it can be used as a physical volume for LVM.

It is particularly useful in host platforms for containers, virtual machines and cloud storage.


Below are the steps to configure VDO on your system.


1. Download the relevant packages

		yum install -y vdo kmod-kvdo
	

2. The size of the block device that will be used should be of minimum 4GB in size. We can create a VDO device like so 

	
		vdo create --name vdo1 --vdoLogicalSize 1T --device /dev/sdd



3. Once the device is created we can create a file system on top of it.


		mkfs.xfs -K /dev/mapper/vdo1


4. Now we need to mount it. The easiest way I found to create an auto mount option is by creating a systemd file for it.
   Dont worry, you wont have to create one from scratch. There is a copy for reference in `/usr/share/doc/vdo/examples/systemd/vdo.example.mount`

   Simply copy that and give it a new name and paste it in `/etc/systemd/system/custom_name.mount


In the file though you need to edit two fields under the \[Mount\] options

		What = /dev/mapper/vdo_device
		Where = /mount/point

Save the changes and enable it using `systemctl`

		systemctl enable --now vdo1.mount


To verify 

		systemctl status vdo1.mount

To further check 

		vdostats --human-readable 


You device is now fortmatted with an XFS file system and will be mounted on boot. 



		
