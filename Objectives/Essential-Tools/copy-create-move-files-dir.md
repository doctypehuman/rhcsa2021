# Copy Create Move Delete Files and Directories 

These are simple basic tasks which need to be mastered inorder to work with large amounts of files or directories. 

##Copy files and directories 

	cp file1 file2 /new/location/where/files/are/pasted

The command *cp* is a powerful command and I would reccomend reading the man page once for this. You can use the *cp* command to create links as well. 
Some common options that can be used with this command are :

- -r Recursive

- -p Preserve file attributes

## Create files and directories 

	touch file #Create a file with the name file 

	mkdir file #Create a directory with the name file 

While creating directories option *-p* is a very useful command. It allows us to create subdirectories within the directory that we have just created. 

	mkdir -p ~/.config/systemd/user


While creating files and directories, globbing can be used to create multiple files and directories.

	touch file{1..10..2} #Will create file1 file3 file5 file 7 file9

	mkdir -p Backup/month_{01..12} #Will create 12 subdirectories while creating the main directory Backup


## Delete Files and Directories 

	rm file #Will remove the file

	rmdir dir #Will remove the directory named dir. This command works only on empty directories

	rmdir -rf dir #Will forecfully and recursively remove directory dir and all subdirectories in it


## Move Files and Directories 

	mv file1 file2 #Will rename the file from file1 to file2

	mv file1 /location/where/the/file/is/to/be/moved/to #will move the file to the new location specified

	mv dir dir1 #Will rename the directory dir to dir1


