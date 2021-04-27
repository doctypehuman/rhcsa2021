## Containers

**This topic has been added in the latest version for RHCSA**

Topics covered here are as follows:

- [Find Containers](#Find-Containers)
- [Inspect Containers](#Inspect-Containers)
- [Container Management](#Container-Management)
- [Run Services](#Run-Services)
- [Configure persistent storage](#Configure-persistent-Storage)
- [Configure container to start on boot](#Configure-container-to-start-on-boot)

**In order to work with contianers you have to download container tools**

	yum module install container-tools

## Find-Containers


Before we dive into to how to find containers, it is important to have a look at the logic of naming container images. This will help you in searching for them.

Container images are named based on the fully qualfied name. 

**registry_name/user_name/image_name:tag**

If you do not put in a tag the system will assume that you want the latest version. 

Container images are found in registries. The list of registries that are available to the user are kept in the location 

	/etc/containers/registries.conf
 

1. registry.redhat.io

This is the official registry where you can find container images maintained by Redhat. You will need a login credentials to download the image. Your redhat login credentials will work fine. 

The command to log in is 
	podman login registry.redhat.io

Once you have logged in you can search and inspect containers. Suppose you want to search for httpd server for RHEL8 you need to type the below command. 
	podman search registry.redhat.io/rhel8/httpd

2. registry.connect.redhat.com

This is the registry that contains container images created by third party vendors and are hosted on Redhat. Suppose you want to search for the RHEL7 version of nginx in this registry.
	podman search registry.connect.redhat.com/rhel7/nginx

3. docker.io

Docker images are compatible with Redhat and there are a host of images that you can search for and download. To find a container image for mariadb here you need to type
	podman search docker.io/mariadb 

4. Local/Remote registry. 

This part is important especially for the exam since chances are very high that a local registry will be made available during the exam. If a local registry is made available to you it has to be configured in the _registries.conf_ file. You need to edit the file and put in the details of the local registry. Below are the steps to do that. 

	vim /etc/containers/registries.conf

	/unqualified #searches for the word unqualified.

Once you have located the unqualified registries you need to enter the details of the registry and uncomment the line in order to enable it. 

	unqualified-search-registries = ['registry.local.com']
	[[registry]]
	location = "registry.local.com"
	insecure = true
	blocked = false

Once that is done you should be good to go. 


So you have found the container image. To pull it you need to simply type in 

	podman pull registry_name/user_name/image_name:tag

An example

	podman pull registry.redhat.io/rhel8/httpd-24

Please note while pulling the container image that if you are pulling the image as an unpriviliged user basically you are not root the containers will be called as rootless containers. Images that are pulled from registries while you are root are stored separately. 

## Inspect-Containers 

One can inspect container images that are stored locally and those that are stored in a registry and are yet to be pulled. 

1. Local Inspection 

Container images that are stored locally can be inspected by 

	podman inspect registry.redhat.io/rhel8/httpd-24


2. Remote Inspection

Container images that are yet to be pulled can be inspected by invoking the _skopeo_ command. If the container image is stored in a registry that needs authentication you need to log in first and then run the command. Inspection using the skopeo command can be done by 

	skopeo inspect docker://registry.redhat.io/rhel8/httpd-24

*Inspection is a great way to find out how the container can used. It will have an example run command and will also inform you of any variables that can be passed to it, in the case of databases for example.*


## Container Management

Now that we have pulled an image from the registry to our host machine, it's time for us to get them containers up and running. If required you can run multiple containers from a single image. Right now we are going to run one container from the *registry.redhat.io/rhel8/httpd-24* image. Containers can be executed in an attached or a detached state. For starting a container in a detached stated we must use the option _-d_ along with the _podman run_ command. The option _--name_ is used to add the name to the container. This can be useful so that you do not have to remember the numeric Container ID. 

	podman run -d --name testweb registry.redhat.io/rhel8/httpd-24

To check if the container is up and running execute the below command 

	podman ps -a

To stop the running container execute 

	podman stop testweb

To remove the container execute 

	podman rm testweb

Should you need to stop multiple containers in one command, please execute 

	podman stop -a

And to remove multiple containers in one go, please execute 

	podman rm -a

## Run Services

There can be a host of services that can be run inside containers. Right now we will run an apache server in a container. This is a good example to showcase how to assign host ports to the container. It is done by using the *-p host-port:container-port* option. It will also give us an opportunity to execute commands in a running container. Let us have a look.

1. Pull the image from the registry

		podman pull registry.redhat.io/rhel8/httpd-24:latest

2. Before running the container, it is important to add the port that we would like to assign. As a non root user you will not be able to assign ports below 1024 for security 
   related reasons. Let us use the port 8080 on the host.

		sudo firewall-cmd --add-port=8080/tcp --permanent

		podman run -d --name myweb -p 8080:8080 registry.redhat.io/rhel8/httpd-24

__please note: when running containers in rootless mode, you cannot assign ports below 1024 due to security reasons.__


3. We need to create the index.html file in the container. Executing commands in a container is done with *podman exec container_name command*
 
		podman exec -it myweb /bin/bash

In the above command we have used the option *-it* which stands for interactive. This will help us enter the container. /bin/bash is what is executed in the container.

	$ touch /var/www/html/index.html
	$ echo "Hello from the container side" >> /var/www/html/index.html
	$ exit

4. Once back in the host machine, we can reconfirm if the container is working

		podman ps 

Now that we have confirmed that our container is running let us check if the ports have been mapped.

		podman port -a

We should get a positive result. Now we can run the command on the host machine to check the output. 

		curl http://localhost:8080/
		Hello from the container side

## Configure Persistent Storage

Local directories on the host machine can be mapped to a directory in the container. This can be useful when running databases or even web servers. Storage is mapped permanently by using the *-v* option. Let us try configuring persistent storage for another container running apache. 

1. Create a directory

		mkdir -p /home/user/web/html/

2. Create the index file and publish some content in it.

		touch /home/user/web/html/index.html;echo "Hello from the container side" >> /home/user/web/html/index.html

_please ensure that appropriate read and write permissions are given to the files, the file index.html shoudl be able to be read by all_

3. Add a port ( please refer to the example mentioned earlier ) 

4. Considering that we have the image already downloaded let us proceed with running the container.

		podman run -d --name web_with_storage -p 8080:8080 -v /home/user/web/:/var/www/:z registry.redhat.io/rhel8/httpd-24

Please pay attention to the *:z* option while mentioning the path to the directory in the container. What it does is, it applies the correct SELinux context to it. 
Please have a look at man podman-run to see more details on it and how it differs from *:Z* option. 

5. Check if the container is up and running. 

		podman ps 

6. Check on your local machine if the settings are correct 

		curl http://localhost:8080/
		Hello from the container side

7. In the above example we have mapped one directory to the container. You can map multiple directories to the container. Each new directory that is mapped has to be given the 
*-v* option. 

## Configure container to start on boot

This can be a little tricky so please be careful. The way to do this is by creating a systemd file for the user. It is done by using *systemctl --user* 
A very important point to note is that you cannot su into the user account to make the changes. You have to directly login as the user. So if you are in the root shell you simply cannot su -user and start configuring. You will have to log out and log in as the user for whom you would want to make these containers start on boot or log in. 

A pro tip is to make create an account that is used primarily for managing containers. 

Let us try to configure the web container that we just created and to which we have added persistent storage. 

1. Login to the users account directly.  *THIS IS A VERY IMPORTANT POINT*  

2. Create the directory /.config/systemd/user in the user's home directory 


		mkdir -p ~/.config/systemd/user


3. Get in to that directory

		cd ~/.config/systemd/user

4. Start the container 

		podman start web_with_storage


5. We will now proceed to generate the systemd files 


		podman generate systemd --name web_with_storage --files


The option *--files* is given so that the output of the command is stored in files. Otherwise the output is simply shared on the screen. 

6. Stop the container 

		podman stop web_with_storage

7. Reload the systemctl --user daemon so that we can force it to read the new configuration files. 

		systemctl --user daemon-reload

8. Enable the new service which is now named container-web_with_storage

		systemctl --user enable --now container-web_with_storage

9. Check the status

 
		systemctl --user status container-web_with_storage


10. We should see the container up and running. Please note that now that we have mapped the container to systemd we should not user podman to start and stop the container. 



11. We are almost done but to ensure that the container is started on boot or login we need to enable linger. This is done by using the loginctl command.

		loginctl enable-linger


12. Enter into root and use systemtl to reboot .

		su - 
		# systemctl reboot 


13. Once the reboot is done , check if the container is up and running. 

		podman ps 


14. To stop the container use systemctl --user 

		systemctl --user stop container-web_with_storage 


In step 5 when we generated the systemd files we can also use the option --new. What this option will do is that each time the container is stopped, it will get deleted and a new container will be started. If you use this as an option be sure to delete the container on which it was based since systemd expects to not find any container when it attempts to start the service.  


