# Restrict Access Using Firewall Cmd

In it's simplest term a firewall is a layer of protocols that are present to regulate incoming and outgoing packets of data.

The regulation of connections is done on the basis of zones. A zone is a collection of rules that are applied to incoming packets matching a specific address or network interface.

Some of the zones that are available are **DMZ** **Public** **Home** **Work**. To get a list of all zones run the below command

		firewall-cmd --list-zones


Each zone has it's own set of protocols. I would not be going into further details of the zones. You can read more about them in the man page.

		man firewalld.zones


Along with setting zones, `firewall-cmd` can be used to add services and ports. This is important for services to run smoothly on the system.


Listing of all services:

		firewall-cmd --get-services

Listing of active services:

		firewall-cmd --list-services

To add a service

		firewall-cmd --add-service=ntp --permanent

We added the ntp service permanently in the above example


To list active  ports

		firewall-cmd --list-ports


To add a port 

		firewall-cmd --add-port=88/tcp --permanent


To implement all changes that have been made we need to reload the daemon.

		firewall-cmd --reload


Also please keep in mind that tab completion will help you guide your commands should you feel lost. 
