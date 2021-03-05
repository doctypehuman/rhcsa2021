# Interrupting boot process to gain access to system.

This method is valid for RHEL / CentOS systems. 

1. Reboot the system.

2. Screen will be displayed with the kernels available. Press spacebar to pause the process.

3. Press e to edit the kernel boot up.

4. Go to the line starting with "linux". Go to the end of that line by pressing Ctrl-e.

5. At the end of the line add "rd.break"

6. Press Ctrl-x

7. The system will now reboot and will take you to the switchroot prompt.

8. Here you must first remount the /sysroot file system with read and write permissions. This is done by typing the below command

	mount -oremount,rw /sysroot

9. Once done change to /sysroot 

	chroot /sysroot

10. Now you can change the root passwd

	passwd root 

11. Configure the system to automatically relabel SELinux context on all files

	touch /.autorelabel

12. Type exit twice to exit and continue the boot process

