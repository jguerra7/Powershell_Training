 # nicknames for commands
Although PowerShell command names can be nice and consistent, they can also be long. A command name such as *Set-WinDefaultInputMethodOverride* is a lot to type, even with Tab completion. Although the command name is clear—looking at it, you can probably guess what it does—it’s an awful lot to type.

That’s where PowerShell aliases come in. An alias is nothing more than a nickname for a command. Tired of typing *Get-Service*? Try this:

```powershell
PS C:\> get-alias -Definition "Get-Service"

Capability      Name
----------      ----
Cmdlet          gsv -> Get-Service
```
Now you know that gsv is an alias for **Get-Service**.

When using an alias, the command works in exactly the same way. Parameters are the same, everything is the same—the command name is just shorter. If you’re used to UNIX or Linux, where an alias can also include some parameters, just know that Power-Shell doesn’t work that way.

If you’re staring at an alias (folks on the internet tend to use them as if we’ve all memorized the hundreds of built-in aliases) and can’t figure out what it is, ask help:
```powershell
PS C:\> help gsv

NAME
    Get-Service
SYNOPSIS
    Gets the services on a local or remote computer.
SYNTAX
    Get-Service [[-Name] <String[]>] [-ComputerName <String[]>]
    [-DependentServices [<SwitchParameter>]] [-Exclude <String[]>]
    [-Include <String[]>] [-RequiredServices [<SwitchParameter>]]
    [<CommonParameters>]
    Get-Service [-ComputerName <String[]>] [-DependentServices
    [<SwitchParameter>]] [-Exclude <String[]>] [-Include <String[]>]
    [-RequiredServices [<SwitchParameter>]] -DisplayName <String[]>
    [<CommonParameters>]
    Get-Service [-ComputerName <String[]>] [-DependentServices
    [<SwitchParameter>]] [-Exclude <String[]>] [-Include <String[]>]
    [-InputObject <ServiceController[]>] [-RequiredServices
    [<SwitchParameter>]] [<CommonParameters>]
    ```
    
    When asked for help about an alias, the help system will always display the help for the full command, which includes the command’s complete name.
    
    
    
