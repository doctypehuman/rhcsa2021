# Basic Bash

Bash is a low level programming language that is very useful for automating tasks. The reason it is a low level language is because it does not need a compiler to process it. 
It is a relatively simple language and once mastered can help in carrying out sysadmin tasks. 

BASH is not the only shell that is available on the system. To list all the shells that are , use the below command. 

		cat /etc/shells

In this document I will not be going over the basics of BASH. For that please check my other repository dedicated to [BASH](https://github.com/doctypehuman/bash)
Also, I would be stating the basic formats of the code here. For example scripts please go [here.](https://github.com/doctypehuman/doctypehuman/bash)

Now let's have a look at the objectives.

- [Conditionally execute code](#conditionaly-execute-code)

- [Use looping constructs](#use-looping-constructs)

- [Process Script Inputs](process-script-inputs)

- [Process output of shell commands from a script](process-out-of-shell-commands-from-a-script)

- [Process shell commands exit codes ](Process-shell-commands-exit-codes)








## Conditionally execute code

Commands written in bash can be executed basis some logic. This is achieved by using the "If Else" syntax.
It goes something like this 

		if some_condition;then
			echo " This echo command executes if the condition above is true"
		else
			echo " The condition is false"
		fi

Please note the beginning if and the end fi. They are necessary. Let me also explain a little bit about conditions and them being true or false. 
Conditions can be a command or a test. A command is considered to be true if it executes without an error. If it gives an error
then it would result in a false result. 

Testing. This is achieved by placing the condition in double square brackets. 

		if [[ $variable -ge 10 ]] 

Here we are testing if the value is assigned to variable is greater than or equal to number 10. There are various different logical operators that are used to check.
Operators for numbers are different to those which are used for strings.


In addition to If Else we can add elif to the block of code. This helps us to further add logic or check for different combinations for the true/false result. 

		if [[ $variable -eq 3 ]];then
		echo " You chose number 3"
		elif [[ $variable -eq 2]];then
		echo " You chose number2 ]]
		elif [[ $variable -eq 1 ]];then
		echo " You chose number 1"
		else
		echo " You got us ! We have no clue"
		fi

Notice for the elif's we do not have to end the block of code with fi. An alternate way to check for multiple combinations is by use the *case* statement. 

		case $option in
			1) command
			;;
			2) command
			;;
			*) command
			;;
		esac

Have a look at my bash repository where I have made a simple calculator using the case statement.



