# Diagnose Correct File Permissions

In order to diagnose correct file persmissions we need to first know the permissions. 

Those have already been discussed earlier under Essential Tools. 

In order to change the permissions we use the command `chmod`

At times we might need to change the owner of the file or the directory. 

For that we use the command `chown`


Syntax chmod:

		chmod 2755 /var/log/journal

In the above example we have assigned to the folder /var/log/journal Set UID , rwx for user, rx for group and other.


Syntax chown

		chown root:systemd-journal /var/log/journal

In the above example we have assigend root as the user and systemd-journal as the group owner for /var/log/journal

If we had wanted to only assign the user the command would have been

		chown root: /var/log/journal

If we had wanted to assign just the group owner, the command would have been

		chown :systemd-journal /var/log/journal

 
