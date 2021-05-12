# Configure Time Service Clients

Time service clients is run by the **chronyd.service** Please ensure that this is installed and enabled.

Once that is done, we need to edit the `chrony.conf` file located in `/etc` directory.

		vim /etc/chrony.conf

In the file we need to add the address of the server with which we would like our machine to be synchronized.
That is basically the first uncommented line in the file which should read pool 2.rhel.pool.ntp.org iburst.

Comment that line out and below that include the server to which you want to be synced. 

Please remember if you are including the name of the server, the name resolution should have been configured i.e the details should be in the `/etc/hosts` file. Else please put in the IP address. 


Once that is done we need to activate the NTP sync. That is done by using `timedatectl` command.

		timedatectl set-ntp true

We can restart the service to implement the changes.


		systemctl restart chronyd.service


To verify our changes we can run the below command.

		chronyc sources



