# Log In Multi User 

There are a few system targets into which we can boot the machine into. For this objective we will discuss only the multi-user.target

To find out which is the current target 

	systemctl get-default


To set multi-user.target 

	systemctl set-default multi-user.target

	systemctl reboot


You will now be given a non graphical interface where different users can login. 


