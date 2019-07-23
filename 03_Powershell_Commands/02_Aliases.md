 # nicknames for commands
Although PowerShell command names can be nice and consistent, they can also be long. A command name such as *Set-WinDefaultInputMethodOverride* is a lot to type, even with Tab completion. Although the command name is clear—looking at it, you can probably guess what it does—it’s an awful lot to type.

That’s where PowerShell aliases come in. An alias is nothing more than a nickname for a command. Tired of typing *Get-Service*? Try this:

```powershell
PS C:\> get-alias -Definition "Get-Service"

Capability      Name
----------      ----
Cmdlet          gsv -> Get-Service
```
