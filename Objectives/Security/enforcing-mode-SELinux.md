# Enforcing Mode SELinux 

This is an important part of the RHCSA objective. Ensure that at the end of your exam, SELinux should be in enforcing mode. 

1. Get the current status of SELinux 

	getenforce

2. If the current mode is permissive, change it by using setenforce and numbe 1 for enforcing 

	setenforce 1

3. Now when you use getenforce you should see enforcing, BUT WAIT ! It's not done yet !! 


4. You need to head over to the SELinux config file located at /etc/selinux/config


5. You need to check what the status is here. It should be SELINUX=Enforcing. If it is permissive. Edit the file and make it enforcing.


6. Reboot the system. Without a reboot the mode change will not occur. 


