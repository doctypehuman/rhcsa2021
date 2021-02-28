# Redirection 

As the name suggests Redirection is the method where the output of a command is redirected. The output can be redirected to be saved in a file or it can be redirected to another command where it becomes the input. To redirect the ouput of one command as an input of another command you need to use pipes *|*. Some basics that need to be known are channels. There are four such channels but we are discussing the basic three. Standard Input, Standard Output and Standard Error. The fourth channel is called filename and is represented by the number 3. 

Stdin is represented by 0.

Stdout is represented by 1.

Stderr is represented by 2. 


It is executed by using these symbols  *>* , *>>* and by using the number associated with the channels. You will see that below in the examples.


### Basic Redirection 

1. Save an ouput of a command to a file. 

	date > timestamp

In the above example the file timestamp will be created if it is not already present. 

2. Append an output of a command to a file. 

	echo ************ >> timestamp

In the above example the contents of the command will be added to the file timestamp. Had we used *>* the earlier contents of the file would have been overwritten.

3. Display the output of the command and save the error messages to a file. 

	find /etc -name passwd 2>redir-errors

In this example the output will be displayed to us while the error messages will be saved in redir-errors.

4. Display command output and ignore error messages.

	find /etc -name passwd 2>/dev/null

The location /dev/null is like the electronic black hole in the system. The error messages will be sent there and you will be displayed the output. 

5. Save output and errors in the same file. 

	find /etc/ -name passwd &> output_plus_error

By using *&>* both the output and errors are redirected to one file. 


6. Append output and errors to one file.

	find /etc -name passwd >> output_plus_error 2>&1 

When using pipes *|* we need to use this option for correct execution. 


### Piping 

This method is applied to use the output of a command as an input for another command.  


1. Basic piping 

	 ls /usr/bin | less


The above example will paginate the result of the ls command. 


2. Multiple piping 

	cat /etc/passwd |  grep user | cut -d "" -f 4

In this example first the cat command will be executed, then grep will run on the output selecting user. After this the cut command will be applied to shorten the result. 


3. Conditional piping 

	cat /etc/passwd && grep random && cut -d "" -f 4

In this example commands mentioned after && will only be executed if the preceding command is executed successfully. 


4. Tee command 

Tee command is used to display the output in the pipe command that are generally supressed. 

	ls -l | tee /tmp/tmp-ls


If you want to append data to a file with *tee* use the *-a* option.

	date | tee sample.txt
	uptime | tee -a sample.txt
 
