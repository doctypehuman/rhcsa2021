# Start and Stop Services On Boot


Services are controlled in Linux with the systemd process which in turn delegates it to the systemctl daemon. 

In order to ensure that services are started on boot the service needs to be set to *enabled*

So if you would like to have the web server running on boot, the command for that would be 

		systemctl enable --now httpd.service


The above command will start the service as well. 

Similiarly if you would want services to not start on boot you need to disable them.

		systemctl disable httpd.service

Once this is done you will have to manually start the service each time the system is rebooted. 
