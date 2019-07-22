# Dissecting the Powershell Command 
Figure Below shows the basic anatomy of a complex PowerShell command. We call this the full-form syntax of a command. 
We’re showing a somewhat complex command so you can see all of the things that might show up.
![image](https://user-images.githubusercontent.com/47218880/61657966-e7257700-ac89-11e9-92df-afed7148dc2c.png)

To make sure you’re completely familiar with PowerShell’s rules, 
let’s cover each of the elements in the previous figure in more detail:

- The cmdlet name is Get-EventLog. PowerShell cmdlets always have this verb-noun naming format. We explain more about cmdlets in the next section.
- The first parameter name is -LogName, and it’s being given the value Security. Because the value doesn’t contain any spaces or punctuation, it doesn’t need to be in quotation marks.
- The second parameter name is -ComputerName, and it’s being given two values: WIN8 and SERVER1. These are in a comma-separated list, and because neither value contains spaces or punctuation, neither value needs to be inside quotation marks.
- The final parameter, -Verbose, is a switch parameter. That means it doesn’t get a value; specifying the parameter is sufficient.
- Note that there’s a mandatory space between the command name and the first parameter.
- Parameter names always start with a dash (-).
- There’s a mandatory space after the parameter name, and between the parameter’s value and the next parameter name.
- There’s no space between the dash (-) that precedes a parameter name and the parameter name itself.
- Nothing here is case-sensitive.

```
Get used to these rules. Start being sensitive about accurate, neat typing. 
Paying attention to spaces and dashes and other rules will minimize 
the silly errors that PowerShell throws at you.

```
 
