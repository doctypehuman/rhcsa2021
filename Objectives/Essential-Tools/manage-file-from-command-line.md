# Manage files from the command line 

- [Linux File System Hierarchy](#linux-file-system-hierarchy)

- [Move Copy Remove](#move-copy-remove)

- [Globbing](#globbing)

- [Expansion Supression Substitution](#expansion-Supression-Substitution)






### Linux File System Hierarchy 

The linux file system is an inverted tree of directories. The reason why it is inverted is because the root directory symbolised by */* is where it all begins. Flowing from that are the other folders or sub-directories. Some of the most important sub directories are mentioned below in no particular order for reference

1. /usr/

This folder contains all the installed software, shared libraries. Important sub folder here are 

- /usr/bin/ 

Contains user commands

- /usr/sbin/

Contains sys admin commands 

- /usr/local 

Contains locally customized software


2. /root/

Is the home folder for the user root.

3. /home/

Is the home folder for the regular user. 

4. /var/

Contains variable  data specific to the system that should persist between boots. Files that dynamically change ( eg databases, cache directories, log files, printer spool documents, web-site content)/

5. /tmp/

Temporary data that will be automatically deleted if it is unmodified or not accessed for 10 days. There is another folder that contains temp data and that is */var/tmp/*. This folder also get cleaned automatically but every 30 days. 

6. /run/

Contains runtime data for processes started since last boot. Contents of this folder are recreated on reboot. 

7. /boot/

Contains files required during the boot process.

8. /dev/

Contains special device files that are used by the system to access hardware.

9. /etc/

Conatins system configuration files specific to the system.

10. /mnt/

Contains mount points for various filesystems.

### Move Copy Remove 

Files and folder can be moved, copied and removed from the command line. The command for move is also used to rename files and folders. 

- Copying files and folders 

	cp file1 file2 /location/where/file/is/to/be/copied

	cp dir1 dir2 /location/where/dir/is/to/be/copied

- Moving files and folder 

	mv file1 and file2 /location/where/file/is/to/be/copied

	mv dir1 dir2 /location/where/dir/is/to/be/copied

- Renaming file and dir

	mv file file_new_name

	mv dir dir_new_name

_Example_

We want to rename file1 to file2

	mv file1 file2

- Removing files and directories 

	rm -rf file_name

	rm -rf dir_name

The options *-r* is for recursive and *-f* is for force

### Globbing

Globbing is basically using a pattern to assist you in specifying different file names. Below are some commonly used patters followed by brief examples. 

_Pattern or Special Character_ and _what it will match_

  \*                                 Any string of 0 or more characters
  
  
  ?                                    Any single character
  
  
  ~          	  		       User's home directory
  
  
  ~+ 				       Current working directory
  
  
  ~-   	 	 	 	       Previous working directory
 
 
 \[abc\] 			       Any one character enclosed in the class
 
 
 \[!abc\]		               Any one character NOT enclosed in the class 
 
 
 \[^abc\]                              Any one character NOT enclosed in the class


\[\[:alpha:\]\]                        Any alphabetic character


\[\[:lower:\]\] 		       Any lowercase character 


\[\[:upper:\]\] 	               Any uppercase character 


\[\[:alnum:\]\] 	               Any alphabet or digit


\[\[:digit:\]\] 	 	       Any digit


\[\[:punct:\]\] 	 	       Any printable character not space or alphanumeric 


\[\[:space:\]\]                        Any one whitespace character may include tabs, whitespace or carriage return or new line


These patterns can be used even in bash and also in grep. 

						
*Example*

	ls [[:upper:]]*

The above command will give a list of only those files or folders which begin with an uppercase letter. 

	ls *[[:digit:]]

The above command will give a list of only those files or folders which end with a digit.

### Expansion Supression Substitution

- Brace Expansion 

This is a useful tool to manage multiple files with one command. 

	touch file{1,2,3}.txt

The above command will give an ouput of file1.txt file2.txt and file3.txt 

Below are some more examples of brace expansion that you can try out to see the output

	touch file{1..100..2}.txt

	touch file{01..100..2}.txt

Notice the difference in the ouput sequencing of the above two commands. 

	touch {a,b}{1,2}.txt

	touch {a{1..10},b,c}.txt

Brace expansion can also be used to identify files or directories  in order to copy or move or delete them. 

	mv file{1,2,3,4} ~/work/brace/


- Supression 

To remove the meaning of a special character eg ? one needs to add a backslash '\' before it. This can be helpful for A character. Should you need to do it for a string you should use double quotes "".


- Substitution 

Command substituotion is useful when you want to use different commands in an existing command. Command substitution occurs when a command is enclosed in brackets preceded by a $ sign.  

Example 

	echo today the date is $(date)



