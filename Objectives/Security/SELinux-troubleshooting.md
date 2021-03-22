# SELinux Basic Troubleshooting 

The most common problems that can arise in SELinux at this level (RHCSA) are files and ports that do not have the correct context assigned to them. 

Both these topics have been covered in different articles. But since this repository is also made for practice, I will repeat both of them here for your reference. 

*Files with incorrect context*

This problem may arise with your apache server or with any other server for which you have changed the default location from which data needs to be sourced. 
For this particular scenario we will have a look at the httpd service. 
Consider that you have changed the document root to /web . Now this new folder and it's contents will not have the correct SELinux context associated with it. 
Below are the steps for you to troubleshoot and get your server up and running. 

1. Find out the right context which needs to be applied. You can do this by looking at the default location and see what context the files have by *ls -Z*
   Alternatively you can check *man -k _selinux*

2. Now that you have the right context it's time to change the context and update it. 

		semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"  #Changes the context of the folder web and all sub-folders in it
									  #+ -a is for add , use -m if you want to modify an existing context	

		restorecon -R -v /web	# Updates the new files and folders with the new context assigned

3. Restart the service 




*New Ports*

Let us say for security reason you want your sshd.service to listen on a different port than 22. The service will not begin till the new port has been added and the correct
SELinux context has been applied. For this examples sake let us change the default port to 443. Below are the steps for you to troubleshoot SELinux for that

1. Add the port with firewall-cmd
		firewall-cmd --add-port=443/tcp --permanent

2. Reload firewall-cmd to effect the changes
		firewall-cmd --reload

3. Find out the correct SELinux context that needs to be applied to the new port

		semanage port -l | grep ssh

4. Add the correct context to the new port 

		semanage port -a -t ssh_port_t -p tcp 443


Please note, all SELinux commands are to be run either with Sudo privelege or as root. 

5. Restart the service

