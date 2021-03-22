# Create Password and Password Ageing


### Create Passwords

Passwords are created by the command *passwd* Usage would be 

		passwd username 


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


