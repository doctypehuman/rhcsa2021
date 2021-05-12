# Identify and Kill Processes


There are two ways of identifying processes. 

We can use the `ps` command or we can use the `top` command. 

It would be wiser to use the `top` command since it will display processes in context wth the amount of cpu usage. 

If we want to kill the process while we are in the `top` command we need to simply press `k` followed by the PID of the process.

In the case of `ps` where we have just the PID we need to use the `kill` command

Example 

	kill -s TERM PID 

It is wiser to use signals like TERM HUP KILL rather than numbers since on different machines the number signals might have different meanings.

Signals are

- HUP : Hangup

- INT : Interrupt Keyboard , `Ctrl c` is it's equivalent

- QUIT: Keyboard Quit

- KILL: Unblockable Kill

- TERM: Terminate . DEFAULT SIGNAL

- CONT: Continue

- STOP: Unblockable Stop

- TSTP: Blockable Stop

