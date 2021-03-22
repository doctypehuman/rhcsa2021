# Configure sudo access

On RHEL systems sudo access is assigned to users by adding them to the group "wheel"

		usermod -aG wheel username

For specific access that might be required to be given to users without giving all Sudo access is by editing the sudoers file in /etc. 

		visudo



