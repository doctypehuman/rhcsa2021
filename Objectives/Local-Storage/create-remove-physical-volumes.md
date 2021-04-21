# Create Remove Physical Volumes

Physical volumes are the building blocks of Logical Volume Managemenent. Creation is relatively straightforward.
While using disks it is considered best practice to make partitions within it. To use a partition that will be 
converted to a physical volume please ensure that the partition type is of LVM. i.e Code 8e for MBR and 8e00 for GPT.


Once the partition is created and written in the disk, creating the physical volume is done by using *pvcreate*

		pvcreate /dev/sdb1

To verify the creation of the physical volume

		pvs

Just like creation, removal of physical volumes is also straightforward. Please ensure that it is not attached to a working Logical Volume or Volume Group.

		pvremove /dev/sdb1


