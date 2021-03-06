# Manage Tuning Profiles

Tuning profiles are manged in RHEL by the *tuned* facility. Check if it available and installed by 

	rpm -q tuned

Then check if is active 

	systemctl status tuned.service

Once it is active the command to use is *tuned-adm*

	tuned-adm list

This will show all the profiles available and the profile that is currently set.

To see which profile is recommended 

	tuned-adm recommended

To set a certail profile 

	tuned-adm profile profile-name


