# Start Stop Status Network Services

In order to manage system services in RHEL we need to use *systemctl*

1. Start a service
		systemctl start httpd.service

2. Stop a service 
		systemctl stop httpd.service

3. Status of a service 
		systemctl status httpd.service

4. Restart a service
		systemctl restart httpd.service 

5. Enable a service to start on boot
		systemctl enable --now httpd.service  # This will start the service as well if the service was not active.

For Network services such as connections we need to use nmcli

1. Start a connection
		nmcli con up enp0s3

2. Stop a connection
		nmcli con stop enp0s3

3. Add a connection 
		nmcli con add con-name "Connection" ipv4.address 10.0.0.0 ipv4.method manual

4. Delete a connection 
		nmcli con del "Connection"

5. Status of a connection 
		nmcli con status Connection

6. Status of active connections
		nmcli con status --active


