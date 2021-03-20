# Key Based Authentication for SSH

We will have a look at 

- [Key Based Authentication](#Key-Based-Authentication)

- [Security for SSH](#Security-for-SSH)

























## Key Based Authentication

Using passwords to login remote systems is a bad security practice. With SSH we can use keys for authentication. 

While we have covered the basics of key generation in the Essentials folder, will briefly touch upon them once again and dive a little deeper. 

You have to have two systems that can ping each other and have sshd installed on both of them. 

For these examples let us consider that we have the user github which is available on both the systems, Remote1 and Remote2. 

1. On machine Remote1 we will generate the keys for user github

			ssh-keygen

This will create a folder .ssh in the home directory of the user and in that folder will store two keys. A public key and a private key. It will prompt you for the location of the key and a passcode to be associated for the key. Simply press enter for each prompt. 


2. We will copy the generated public key to Remote2. If you have generated the keys for the first time you will not have to specify the key that needs to be copied.

		ssh-copy-id github@Remote2

You will be prompted for the password for the user since this is your first login. Once you type the password you will be given access to user github on Remote2 and the key will be copied. 


3. Type exit on Remote2 and close the ssh connection. We will now generate a fresh pair of keys, ones which have a password associated with them.


4. Generating the new set of keys

		ssh-keygen -f ~/.ssh/key2

We have used the option -f to specify the name and the location of the new key. Now when you generate this pair of keys, issue a password to be associated with it. 


5. We are going to copy this particular key now to Remote2

		ssh-copy-id -i ~/.ssh/key2.pub github@Remote2

You will not be asked for a password here since you have already copied a set of keys. 


6. Type exit to close the connection.


7. We will now use the new key once again to gain access to Remote2. This time we should be prompted for the password associated with the key.

	ssh -i ~/.ssh/key2 github@Remote2

We will have to type in the password for the key to gain access to the system. This will happen each time you use this key. There is a way to by pass this. 


8.  Type exit to close the connection.


9. On Remote1 run *ssh-agen* in your bash shell and add the key with which a password is associated. 

		github@Remote1$ eval(ssh-agent)
		Agent PID 1234
		github@Remote1$ ssh-add .ssh/key2
		Enter passphrase for .ssh/key2: password
		Identity added .ssh/key2

When we ran eval it configured ssh-agent for this session to use it. We then used ssh-add to add the private key to ssh-agent. We can now use the password protected key without typing in the password to gain access to Remote2

		ssh -i ./ssh/key2 github@Remote2 hostname

This method is shell session specific. If you exit this session you and you use the key again you will be prompted for a password. 








## Security for SSH 

The basic steps that one can take to increase the security of SSH are 

1. Disable ROOT login. This can be done by editing the config file /etc/ssh/sshd_config 

2. Disable password authentication  This can be done by editing the config file /etc/ssh/sshd_config 

3. Limiting the users that are allowed to use SSH to access. This can be dony by adding a line "AllowUsers" OR "DenyUsers" in the config file. 

4. Changing the default port. We will have a look at this in detail.

Since it is common knowledge that port 22 is used for SSH we can increase our increase our security by using a different port. Let's have a look at how we can do that. 

In the below example we are going to use port 443. This port is generally used for web servers that allow TLS.  

1. Add the port with firewall-cmd 

		firewall-cmd --add-port=443/tcp --permanent


2. Check for the correct SELinux context that is assigned for SSHD and then assign that to the new port 

		semanage port -l | grep ssh  #Find the correct context that needs to be applied

		semanage port -a -t ssh_port_t -p tcp 443  #Adding the contect ssh_port_t on port number 443 which is tcp. -a is used for addition. -m will be used if there is an existing context and if it needs to be modified. 


3. Edit the sshd_config file so that it now listens on port 443 and now on 22

		vim /etc/ssh/sshd_config
		Port 443

4. Restart the service 

		systemctl restart sshd.service

If correct SELinux context is not applied to the port, the service will not start. 










