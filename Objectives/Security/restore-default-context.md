# Restore default file context

Well we have already learnt about context birefly. We will now see how we can change them and how to restore them. 

The way SELinux works while changing context is that at first you need to ask it to change the context. And then once you have changed it ( the context ) you need to tell SELinux to restore it. By that it means that you are informing SELinux that you have changed the context and want it implemented. Treat it like if you have changed parts of a configuration file of sshd. You will need to restart the service to implement the changes. It's something like that. 

The classical example for changing SELinux context and restoring them is the Apache web server. 

For this we are going to change the location of the Document Root in the Apache configuration file. 

1. First make a folder in your home directory called web. In that make a sub directory called html and in that create an html document called index.html and put some text in it.

		mkdir -p ~/web/html
		touch ~/web/html/index.html
		echo " If you see this, you updated the SELinux context correctly"

2. Now we change the root document in our apache config. This has to be done with sudo privelege. Stop the server first in case it is running. 

		sudo systemctl stop hhtpd.service
		sudo vim /etc/httpd/conf/httpd.conf

3. Now in the configuration file find DocumentRoot and change it to ~/web

4. Once done check look for #Relax access to content within /var/www/ . Make changes so that it look like what is typed below

		<Directory "~/web">
		Allow Override None
		Require all granted
		</Directory>

5. These changes are important else it will be Apache that will restrict access and not SELinux ! 

6. Go to ~/web/ and run ls -RZ to see the SELinux context.

7. Restart the apache server for the configuration to take effect

		sudo systemctl restart httpd.service

8. Check if you can see the contents from the new index.html

		curl http://localhost:80/

9. You will not be able to see it since SELinux is preventing from the page loading because it does not have the right context. 

10. Set SELinux to permissive for troubleshooting . You can also stop the server.

		setenforce 0; sudo systemctl stop httpd.service

11. It's time to change the context of the local folder so that you get to see the changes. Before you change the context, you need to find out the correct context.
    Go to /var/www/html and *ls -z* to see the context that is applied there.

12. Come back to your web folder and run the below command 

		sudo semanage fcontext -a -t httpd_sys_content_t "~/web(/.*)?"

13. We have told SELinux to change the context of the folder web and all it's sub folders to httpd_sys_content_t . Now we need to tell SELinux to implement it .

		sudo semanage restorecon -R -v ~/web	

14. Set SELinux back to enforcing mode 

		setenforce 1

15. Start the server 
		sudo systemctl restart httpd.service

16. Check for the new contents

	curl http://localhost:80/

17. You should be able to see the new contents now .

 	
