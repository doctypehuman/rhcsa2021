# Process Scheduling

A user can request the system to carry out certain tasks which are either repetitve in nature or those that have to be executed at a pre defined time.

For tasks that need to be carried out repeatedly we can use *cron.* For tasks that are not to be repeated but are a one time execution we use *at.*



## Cron 

Cron is managed by the _crond.service_ Tasks are created in the crontab. At first we need to check if the service is up and running.

		systemctl status crond.service


Once we confirm that the service is enabled and running we can proceed to create a crontab.

		crontab -e

This is will create a crontab for the current user. It is basically an empty file in which the instructions have to be put in. 

A Crontab will contain 5 basic values followed by the command that needs to be executed.

1. Minutes 0-59

2. Hours 0-23

3. Day of Month 1-31

4. Month 1-12

5. Day of the week 0-7 ( 0 and 7 both signify Sunday, alternately you can use first three letters of the day, eg Mon, Tue etc)


Keeping these values in mind a simple crontab will look something like this 

		0 11 * * 1-5 some_script # some_script will get executed at 11:00 am on weekdays only

		* * * * * some_scrtipt # some_script will get executed every minute

		*/2 * * * * some_script # some_script will get executed every two minutes

		0 */2 2 12 5 some_script # some_script will get executed every two hours on 2nd december and on every Friday in December


To create a specific crontab for a user the *-u* option is used followed by the username.

		crontab -e -u username


To view the current cron jobs

		crontab -l

To delete cron jobs

		crontab -r

## At

At is used for non recurring jobs and is managed by the atd.service. 

There are two ways of creating jobs with At.

1. Use piping 

			echo "Hello" >> at.txt | at noon

2. Classic Format
			
			at noon
			>echo "Hello" >> at.txt
			>Ctrl+D
			
You might have noticed that we used noon to signify time. Here are some more examples of different timespecs that can be used. For the complete list, please refer man pages.

- now +5min
- teamtime tomorrow (4:00pm tomorrow)
- noon +4days
- 5pm April 28 2021

To view the current jobs use the command *atq*

To inspect the actual job use
	
			at -c <jobnumber>

To remove a job use 

			atrm <jobnumber>
