# Extend Existing Logical Volumes


There are different commands to execute the extension of existing Logical Volumes.

- lvextend : Allows addition

- lvreduce : Allows removal

- lvresize : Allows both addition and removal

Amongst them I prefer using the last command as it allows us to add or remove space in a single command.

Some points to remember before executing this command 

1. XFS file systems cannot be reduced. Ext4 can

2. In case of increasing the size of the logical volume, the volume group that it is based on should have available space.

3. In the process it is wise to use the option **-r** since with this option the file system on the logical volume is also resized.

4. Option **-L** is used to specify absolute size. It will be expressed in M,G etc

5. Option **-l** is used to specify logical extents.


Increase in Size

		lvresize -r -L + 1G /dev/volume_group/logical_volume

Decrease in Size

		lvresize -r -l 10 /dev/volume_group/logical_volume


