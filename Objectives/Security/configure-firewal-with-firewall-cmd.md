# Configure Firewall with firewall-cmd

Firewall-cmd is the utility that allows us to set up firewalls around the system. What it means is that you can limit traffic to and from the system. It works on the basis of predefined set of rules known as Zones. In addition to this it also works on Services. Root or an account with sudo privileges can execute commands with firewall-cmd. 


## Zones


To get a list of all pre-defined zones

	firewall-cmd --list-all-zones

Some basic and important zones that you could/should be aware of are:

1. DMZ : Referring to the demilitarized zone, this zone carries strict rules for the system. Only selected incoming connections are accepted.

2. BLOCK: Only network connection initiated within the system are allowed.

3. DROP: Only outgoing connections are allowed. Incoming connections are dropped without any explanation.

4. EXTERNAL: Selective incoming connections are allowed. This is more trusting than DMZ. Used for routers.

5. HOME: Trust other systems on the same network. 

6. INTERNAL: Trust all systems on the same internal network.

7. PUBLIC: For use in public area or public networks where you do not trust other systems present on the network.

8. TRUSTED: All connections allowed. 

9. WORK: Where you trust some of the systems on the network. 

The default zone assigned to an interface is public.



Firewall-cmd is a command that can be completed with bash completion. That is you can use 'tab' to list all the possible combinations of the command. 

To see if firewall-cmd is running 

	firewall-cmd --state

The use of Zones is important when the server has multiple interfaces. Each interface can be assigned a specific zone. I am not going to list all the zones here. The first command that I mentioned should give you all the zones with its properties. Pipe it into *less* to read it carefully. 

Let us have a look at assigning different zones to different interfaces. 

List available interfaces 

	firewall-cmd --list-interfaces

In case no interface has been added, you can add them and assign them a zone

	firewall-cmd --add-interface=enp0s3 --zone=public


To see what zone is currently active

	firewall-cmd --get-active-zone


To assign an interface to a new zone 

	firewall-cmd --zone=home --change-interface=enp0s3 --permanent


To set a new default zone 

	firewall-cmd --set-default-zone=home

## Services

Along with zones there are services that are used to limit the connections that are allowed to and from the system. 

To get a list of active services 

	firewall-cmd --list-services


To get a list of all services 

	firewall-cmd --get-services


To add a service 

	firewall-cmd --add-service=ftp --permanent


This is basic information regarding services. In addition to this you can configure local services. That is as of now out of scope of this document. Having said that though
it is important to note that each service has a corresponding XML document that can be found in */usr/lib/firewalld/services*





