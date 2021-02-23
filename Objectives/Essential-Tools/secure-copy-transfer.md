# Securely copy and transfer files. 

This is relatively straight forward. The system uses SSH protocol for this method. Therefore it is necessary that the remote system that you wish to log in is saved in your ssh key for the user account that you will be using. 


## Copying 

The command to be used is *scp* and the format for copying files from the host system to the remote system is 

	scp /path/to/file(s)/that/need/to/be/copied remote_host_name:/locatio/of/file/to/be/copied

As an example consider that the host system has the name host and the remote system's name is remote. You want to copy the file transfer.txt which is located in the user's home directory. You want to copy these files in the home directory of user in the remote system.

	scp /home/user/transfer.txt remote:/home/user/

Now for the reverse case where in we want to copy the files from the remote host to local. This command is again being typed on the host system.

	scp remote:/home/user/transfer.txt /home/user/


## Secure Transfer

The command to be used is *sftp* . Through this command one can upload and download files from another system. Once again ssh is used for this method so the ssh key should be already saved. In this command if you do not specify the user then the system will assume the current user that is logged in. Once you have invoked *sftp* you need to use *get* to download and *put* to upload. While using *sftp* one can use commands like *pwd, cd, ls, mkdir, rmdir* Once done you can type *exit* to exit from *sftp*

An example for upload of files.

	sftp remote
	>mkdir test
	>cd test
	>put /home/user/transfer/files
	>exit

An example for download of files. 

	sftp remote
	>get /home/user/transfer/files



