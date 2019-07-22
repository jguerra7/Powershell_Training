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
 
## The cmdlet naming convention

First, let’s discuss some terminology. As far as we know, we’re the only ones who use this terminology in everyday conversation, but we do it consistently, so we may as well explain:

- A **cmdlet** is a native PowerShell command-line utility. These exist only inside PowerShell and are written in a .NET Framework language such as C#. The word cmdlet is unique to PowerShell, so if you add it to your search keywords on Google or Bing, the results you get back will be mainly PowerShell-related. The word is pronounced **command-let**.
- A **function** can be similar to a cmdlet, but rather than being written in a .NET language, functions are written in PowerShell’s own scripting language.
- A **workflow** is a special kind of function that ties into PowerShell’s workflow execution system.
- An **application** is any kind of external executable, including command-line utilities such as Ping and Ipconfig.
- **Command** is the generic term that we use to refer to any or all of the preceding terms.
Microsoft has established a naming convention for cmdlets. That same naming convention **should** be used for functions and workflows, too, although Microsoft can’t force anyone but its own employees to follow that rule.

The rule is this: Names start with a standard verb, such as **Get** or **Set** or New or Pause. You can run **Get-Verb** to see a list of allowable verbs (you’ll see about 100, although only about a dozen are common). After the verb is a dash, followed by a singular noun, such as Service or Process or EventLog. Developers get to make up their own nouns, so there’s no **Get-Noun** cmdlet to display them all.

