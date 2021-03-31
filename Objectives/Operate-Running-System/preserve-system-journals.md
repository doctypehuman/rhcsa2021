# Preserve System Journals

Logs by default are not deleted after a specific number of days by the logrotate facility. In order to make them permanent one needs to make certain changes. There are two ways 
of going about this. 

1. Create a new storage.conf file

		mkdir /etc/systemd/journald.conf.d/
		cat << END > /etc/systemd/journald.conf.d/storage.conf
		> [Journal]
		> Storage=persistent
		> END
		systemctl restart systemd-journald

What we did here is create a new file _storage.conf_ which instructs journald to keep the logs. After that we restarted the service for the changes to take place.


2. Create a folder in the /var/log directory 

		mkdir /var/log/journal/
		chown root:systemd-journal /var/log/journal
		chmod 2755 /var/log/journal
		killal -USR1 systemd-journal


To check if the logs are preserved

		journalctl -b  # show logs since last boot


