# SELinux Context 

Security Enhanced Linux. This was developed by the National Security Agency of USA i think in the late 90's and was eventually adopted by Linux in the early 2000's.
In a nutshell SELinux provides assistance in providing / restricting access to files on the system. It does not help in authentication. 

There are two ways in which SELinux restricts access to files. Targeted and Layered.

Layered is way out of scope of RHCSA but to give you an idea it works on access given to different users who have different access limits depending on their security clearance. For example the National Security Agency of USA. 

Targeted is when each file is assigned certain values by SELinux basis of who owns the files or for what are the files meant for. This can be applied to files, ports , users etc.
I am not so well versed with the topic. I know the objectives of the exam and I have built my knowledge around that. 

So since Layered is out of scope we will be focussing only on Targeted. Before we do that it is important for us to know some basic building blocks of SElinux


1. Policy : Consider this to be the set of rules that SELinux follows on the system. 

2. Source Domain: User or process that is trying to access a file or port

3. Target Domain: File or port that the user or process is trying to access

4. Context: Security label that is assigned to a file or port. It categorises Objects for SELinux

5. Rule: Part of SELinux which determines who can access what

6. Labels: These are on files and ports and help us identify the connection between source domain and target domain

To have a look at what are the SELinux context values in a directory, execute


		ls -Z 


The context values are always made up of three aspects.Role, Object and Type.

Context is changed by *semanage* which is not always present by default. 
To find out the package that has it please run the below command

		yum whatprovides */semanage

Once you have downloaded the package you can start listing and chaning contexts. 
 



