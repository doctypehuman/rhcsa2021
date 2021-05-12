# Create Set GID Directories

Set GID directories are thos directories that have been assigned special Set GID permissions. 

This sort of permission is used for collaboration between different users.

What this permission basically does is that all files that are created or edited are given group ownership of the directory. 

In the octal form we need to assign the number 2 to assign it and in the symbolic form we need to use g+s


Example 

		chmod 2755 /groups


Symbolic Example
		
		chmod g+s /groups


