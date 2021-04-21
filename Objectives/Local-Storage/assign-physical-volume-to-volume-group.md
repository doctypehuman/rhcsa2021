# Assign Physical Volume to Volume Group

Volume Groups are the second step in creating a logical volume. Volume groups are made of physical volumes.
We will have a look at creating Volume Groups which in turn will automatically assign the physical volume to it.


Creation is done like so

		vgcreate vgdata /dev/sdb1

In the above command vgdata is the name of the volume group that we gave to the new created volume group. 


Extending a Volume Group is also a useful and important task that one should be aware of. It helps us in extending the Logical Volume if the need arises. 


Extension is done like so 

		vgextend vgdata /dev/sdb2

Removal of a volume group is done like so

		vgremove vgdata

Before removing a Volume Group please ensure that no Logical Volume is attached to it to avoid data loss. 

 
