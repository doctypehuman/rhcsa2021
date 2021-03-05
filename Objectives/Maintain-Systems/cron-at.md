# Automating tasks with Cron and At.

Linux offers programmes that assist us in automating various tasks. For tasts that are repeated frequently we can use *cron.* For tasks that are not repeated frequently but are a one off task that are to be done in the foreseeable future we use *at.*


### Cron 

Cron is conrolled by the crond.service This service is generally up and running on boot but nonetheless you can check it's status by running 

	systemctl status crond.service

Cron jobs are created by editing the crontab. That is done by the below command.

	crontab -e 

To see existing cron jobs

	crontab -l 


