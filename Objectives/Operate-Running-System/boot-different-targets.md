# Boot Different Targets

Targets are nothing but a collection of units which are basically files that work together. A target can also be described as a collective state that the machine can be in.

The basic targets that can be used in Linux are 

- emergency.target :  When activated the machine is started with the bare minimum services required for it to function. 

- rescue.target	   : All services except non-essential services are activated.

- multi-user.target: Generally the default target for servers. Has a command line interface.

- graphical-target : As the name suggests you are presented with a GUI, used for desktops.


The system as such has a default target that is assigned and that can be changed. 

To see which target is activated


		systemctl get-default


To set a new or a different default target

		systemctl set-default multi-user.target


While this is the way to set default targets, there can be a situation where you would want to change the machine state for troubleshooting. 

If you want to change the target during boot, you need to edit the boot menu. On start up when you are presented the kernels to choose, press the `e` button to enter the boot menu.

Look for the line beginning with Linux. At the end of the line append `systemd.unit=desired.target` Press `Ctlr x` to start the boot process.


Another method of changing the current target is by isolating the target. To find out the targets that can be isolated run the below command

		grep Isolate /usr/lib/systemd/system/*.target

And then run this command to change the target 

		systemctl isolate desired.target


