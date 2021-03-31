# Securely transfer files using SCP Or SFTP

SCP and SFTP are  protocols that uses SSH to securely transfer files to and from host to remote or vice versa. 

SSH keys should be in place for the command to execute without error. While *SCP* works pretty much like th *cp* command , *SFTP* works in an interactive mode and like FTP.

- SCP

1. Copying files from host to remote

		scp /path/to/file remote_host: /location/of/file

2. Copying files from remote to host

		scp remote_host:/path/to/file /location/of/file

- SFTP

1. Putting files from host to remote_host

		$ sftp user@remote_host
		sftp> mkdir hostbackup
		sftp> cd hostbackup
		sftp> put /etc/hosts
		Uploading /etc/hosts to /home/user/hostbackup/hosts

2. Getting files from remote_host to host

		$ sftp user@remote_host
		sftp> get /etc/yum.repos.d/yum.repo
		Fetching /etc/yum.repos.d/yum.repo to yum.repo

Type *exit* to end the session.

