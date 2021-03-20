# Access Control List 

Access Control List or ACL are a way in which we can assign permissions which go beyond the normal user,group and other permissions.

In order to assign them we have to use the *setfacl* command. But before we set them it is wise to see what the existing ACL are. 

That is done by *getfacl* . ACL can be applied to a file or a directory. It is generally applied to directories to give additional permissions to users and groups. 

- Finding the current ACL

		getfacl dir

		getfacl file


- Setting an ACL for user Joe

		setfacl -m u:joe:rwx /dir # -m is for modify , u stands for user which can be replaced with g or o. rwx are the persmissions that are granted for /dir

- Setting an ACL for group collab

		setfacl -m g:collab:rwz /dir

- Setting an ACL so that all access to others is blocked from the dir

		setfacl -mR d:o:--- /dir  # -R is used for recursive so that future directories also have the same setting. d is used for default

If you want to use ACL to configure access for multiple users or groups in the same directory. You have to use ACL twice. First use setfacl -R -m to modify current files and 
then use setfacl -m d: to take care of the additional files that will be created in the directory.


Another important point to remember is the order of permissions that you set. 

1. Set normal permissions

2. Set ACL permissions 


 
