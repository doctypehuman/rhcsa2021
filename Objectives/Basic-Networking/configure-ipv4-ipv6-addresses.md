# Configure ipv4 and ipv6 Address

Connections are managed in RHEL by the network-manager. The command line client for this is *nmcli.* There are other options that are available but I prefer this because you can tab the hell out of it and it is faster.



## Adding a connection 

		nmcli con add con-name static ifname eth0 type ethernet ipv4.address 10.0.0.1/24 gw4 10.0.0.0 connection.autoconnect no ipv4.method manual

Modifying it to add a dns address

		nmcli con mod static ip4.dns 1.1.1.1

Adding a secondary dns address

		nmcli con mod static +ip4.dns 8.8.8.8

Removing the primary dns

		nmcli con mod static -ip4.dns 1.1.1.1

If a plus sign is not mentioned then the current address will be replaced instead of appending it .


Similarly the same can be done for ipv6 addresses.

A great place to look for help should you feel stuck with nmcli is 

		man nmcli-examples


### Basic nmcli commands

After making changes to a connection, for the changes to take effect 

		nmcli con up static

Reload all connection settings
	
		nmcli con reload

List connections

		nmcli con show

List active connections

		nmcli con show --active

Stop a connection

		nmcli con down static

Remove a connection

		nmcli con del static


An important point in setting dhcp and static connections to be noted is that while adding a dhcp connection you must mention ipv4.method auto where as in static it should be manual.


