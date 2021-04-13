# Configure Hostname

To change the hostname on the machine type in the below command

	hostnamectl set-hostname newname

It's that simple. After that you can check by

	hostnamectl status

## Hostname Resolution

While reaching out to other hosts on the network to use their hostname rather than their IP Address you can add their names in the /etc/hosts file.
However to be able to reach them you must also have DNS services configured. That can be done by using *nmcli.* That is explained in another write up.
The hosts file mainly has to contain two pieces of data. The IP Address and the hostname to which the address belongs. In case you are using the 
Fully Qualified Domain Name then the alias hostname can come after that. 

		echo "10.0.0.1 myhost" >> /etc/hosts

OR with FDQN and alias 
		
		echo "10.0.0.1 host.example.com myhost" >> /etc/hosts


