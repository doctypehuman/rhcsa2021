## Containers

**This topic has been added in the latest version for RHCSA**

Topics covered here are as follows:

- [Find Containers](#Find-Containers)
- [Inspect Containers](#Inspect-Containers)
- [Container Management](#Container-Management)
- [Run Services](#Run-Services)
- [Configure persistent storage](#Configure-persistent-Storage)
- [Configure container to start on boot](#Configure-container-to-start-on-boot)


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
	podman search registry.connect.redhat.com/Rhel7/nginx

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


