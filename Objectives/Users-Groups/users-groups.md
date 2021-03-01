# Users and Groups 

Users and groups are controlled via the commands *useradd* , *groupadd* , *usermod* and *groupmod*

I am listing the basic options that are available for user and group creation. For more options please check 

	useradd --help 

and 

	groupadd --help


Before we dive into the creation and modification it is important to have a look at */etc/login.defs* This is the file that contains global settings for password aging and for UID and GID. 

When a user or a group is created an ID is associated with it . For users it is UID and for groups it is GID. When a user is created a primary group is automatically created with the user's username. The user can then be added to supplementary groups. Now let us add a users called github. 

_the UID and GID for the user root is 0_

	useradd github 

If you would like to specify the UID on creation use the *-u* option to specify the UID. A range of UID's have been earmarked by the system, you can check them at /etc/login.defs

Adding a group 

	groupadd hubgit

Once a user or a group has been addedd you can modify them as well. Let's add user github to the group wheel so that it can get admin privelege.

	usermod -aG wheel github

The option *-a* is used to append. *-G* was used to identify the supplementary group to which the user was to be added. 

There are quite a few options that are available for modification. Would reccomend you having a look at usermod --help and groupmod --help . 

Now if you have to remove a group or a user you can do that by using the commands *userdel* and *groupdel* . Please keep in mind that if a user is to be deleted you should use the 
option *-r* so that all files that were owned by that user are removed as well. If this is not done there can be information leaks as the next user that is added would be given the earlier user's UID if not specified and will have access to the files. 

To check for files that are not owned by anyone you can use the below command. 

	find / -nouser -o -nogroup 2>/dev/null 


### Managing passwords 

Passwords are stored in the file */etc/shadow.* It has 9 fields spearated by *:* They are 

1. Login Name
2. Encrypted Password 
3. Date of Last Password Change
4. Minimum number of days before password has to be changed. 
5. Maximum number of days before password has to be changed.
6. Warning period 
7. Number of days an account remains active after a password has expired.
8. Account expiration date ; no of days since 1970.01.01
9. Blank ( for future use )

### Password Aging 

The command to set password aging is *chage* and it can be executed only with root access. 

This is an interactive command and will prompt you for vlaues that are to be filled in once you type the command. 

	chage github 

Or you can specify the options in the command . The options are 

1. -d : last change date ( if kept zero, the user will be forced to change the password on initial login ) 
2. -m : minimum number of days for password to be changed
3. -M : maximum number of days for password to be changed
4. -E : Expiration date of the account 
5. -W : Warn days before expiry of password
6. -I : Inactive days 

If you want to set any of these options globally you must edit /etc/login.defs 

Tip : To calculate X number of days in the future 

	date -d "+ Xdays"



