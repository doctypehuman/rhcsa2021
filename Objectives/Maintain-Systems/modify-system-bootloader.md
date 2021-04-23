# Modify System Boot Loader


GRUB2 is the boot loader for linux systems. You can have a look at the contents of the file at `/etc/default/grub`

Any changes that you would like to make have to be made here. Generally changes are not required however for the purpose of the execercie we will make some changes.

In the file there are 8 lines. Of these line the one starting with GRUB_CMDLINE_LINUX is the most important one. The last two words in the like are rhgb and quiet. 

What these words do is that they supress all the messages from the system during the boot process. Let's remove them so that we can see the messages during boot.

Remeber that these changes can be made only as root user. Once you have made the changes we need to reload the file. We can do that with the below command.


		grub2-mkconfig -o /boot/grub2/grub.cnf



What the above command does is that it regenrates the grub file and saves the output in the grub configuration file in the /boot directory. 

Once that is done you can reboot to see the changes being reflected. 


