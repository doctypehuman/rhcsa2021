# Manage Layered Storage

Layered storage is achieved in RHEL by using STRATIS. What it does is that it presents itself as a much larger file that it actually is. 
The setup of STRATIS is such that the first step is in creating a pool which is based of a block device. The file system is then created on top of the pool.
 The minimum size of the block device should be 1GB. Each STRATIS file system occupies a minimum of 512MiB even if no data has been copied to the file system.


The default file system that is used on STRATIS is XFS. Also when creating a STRATIS device no size is specified. Each file system can grow 
up to the size of all the available storage spaces in the pool.

Below are the steps to create a STRATIS device. 

1. yum install -y stratis-cli stratisd

2. systemctl enable --now stratisd.service

3. systemctl status stratisd.service

So the service is up and running, it's time to create the device. 

4. stratis pool create pool1 /dev/sdc

We have created a pool with the name pool1 in the above command.

5. stratis pool list

6. stratis filesystem create pool1 stratis1

We have created a file system called stratis1 on the pool called pool1.

We do not need to format or specify the size of the file system, we do need to mount it.

7. mkdir /stratis1

Created a mount point and now we need to get the UUID to make the relevant entry in fstab.

8. lsblk --output=UUID /stratis/pool1/stratis1


9. Edit the fstab so that it looks like this 

		UUID=xxx /stratis1 xfs defaults,x-systemd.requires=stratisd.service 0 0 

Once you save the changes run the below commands to execute the changes

		systemctl daemon-reload

		mount -a

10. You can confirm the mount with 

		mount | grep stratis

Also you can run `lsblk` to reconfirm. 


To add additional block devices to your existing pool run the below command.

		stratis pool add-data pool1 /dev/sdd


Another useful feature of STRATIS is using snapshots.

Creation of a snapshot is done with the below command. 

		stratis filesystem snapshopt pool1 stratis1 stratis1-snap

Manually mount the snapshot to see the files

		mount /dev/stratis/mypool/stratis1-snap /mnt


