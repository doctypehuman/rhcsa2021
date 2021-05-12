# Mount Unmount NFS File Systems

Configuring the NFS file system is out of scope of the exam but none the less I will briefly list the steps so that you can set it up to practice.

		yum install -y nfs-utils
		firewall-cmd --add-service=mountd
		firewall-cmd --add-service=nfs
		firewall-cmd --add-service=rpc-bind
		firewall-cmd --add-service=rdp
		firewall-cmd --relaod
		mkdir /nfsdata 		# The directory that needs to be exported
		vim /etc/exports
		/nfsdata  *(rw,sync,insecure,no_root_squash)	# This is what you put in the /etc/exports file
		systemctl restart nfs-server

The above steps will help you set up your nfs server.

In order to verify 

		showmount -e localhost


Assume that all the above steps were taken on server1. Now on server2 we need to install **autofs** to enable automount.


Before we begin with installing autofs we should install nfs-utils on this machine as well to check if the exported directory is available to us.

Checking if the export directory is available

		showmount -e server1


Now we begin installing autofs


		yum install -y autofs
		
Once done installing we need to edit the `/etc/auto.master` file.
Right in the beginning of the file you will see `/misc  /etc/auto.misc`
Below that insert the following `/nfsdata  /etc/auto.nfsdata`

Save and exit the file. 

Now create the file `/etc/auto.nfsdata`

In that file insert the following `files -rw server1:/nfsdata`

Save and exit the file.

Create the mount point `/nfsdata`

Enable and start the service

		systemctl enable --now autofs

 To access the exported directory

		cd /nfsdata/files



The above procedure is used to automount the shared directory. 


We can unmount the directory by disabling the service or if the shared the directory was mounted manually i.e by using the **moun** command,
we can use **umount** to unmount it.


