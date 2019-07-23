The pipeline: connecting commands
In chapter 4, you learned that running commands in PowerShell is the same as running commands in any other shell: You type a command name, give it parameters, and hit Enter. What makes PowerShell special isn’t the way it runs commands, but the way it allows multiple commands to be connected to each other in powerful, one-line sequences.

6.1. Connecting one command to another: less work for you
PowerShell connects commands to each other by using a pipeline. The pipeline provides a way for one command to pass, or pipe, its output to another command, allowing that second command to have something to work with.

You’ve already seen this in action in commands such as Dir | More. You’re piping the output of the Dir command into the More command; the More command takes that directory listing and displays it one page at a time. PowerShell takes that same piping concept and extends it to greater effect.

PowerShell’s use of a pipeline may seem similar at first to the way UNIX and Linux shells work. Don’t be fooled, though. As you’ll come to realize over the next few chapters, PowerShell’s pipeline implementation is much richer and more modern.
