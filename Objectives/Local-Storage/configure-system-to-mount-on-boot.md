# Configure System To Mount On Boot

In order to configure the system to mount on boot one needs to make certain entries in the fstab file which is located in the /etc directory.

While there are existing entries to refer to I will break them down for better understanding. They are listed here in the order they need to be written.

1. What : UUID goes here.


2. Where : Mount Point goes here


3. Type : File System type eg XFS,swap,ext4 etc..


4. Mount Options: Generally defaults but for advanced storage options like stratis and vdo additional information is required.


5. Dump Support: Either an option of 0 for no and 1 for yes.


6. Automatic Check : Options vary from 0 for no ,1 for yes and used to imply that the file system is root and 2 for yes for all other file systems. 


An example for a simple xfs system will look like this

		UUID=8emo20wrmkwr02klskf /mount_point xfs defaults 0 0


An example for a stratis storage device would look something like this

		UUID=8eak442lk4242424 /mount_point xfs defaults,x-systemd.requires=stratisd.service 0 0


