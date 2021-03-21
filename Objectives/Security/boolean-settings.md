# Boolean Setting in SELinux

Booleans are a way of overriding the rules that are set in the policy of SELinux. 

To get a list of current booleans

	getsebool -a

To narrow down the list of booleans you can use grep 

	getsebool -a | grep httpd

To change the setting of a boolean from on to off simply

	setsebool -P logrotate_read_inside_container on 

Reconfirm your actions are reflecting in the system 

	getsebool logrotate_read_inside_container


