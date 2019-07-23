
# Getting help
Gaining confidence using the built-in help system is an important part of working with PowerShell. In PowerShell, help is extensive; authors can easily write their own help content when working with scripts and script modules.

A number of commands are available to interact with the help system, as follows:
```
Get-Help
Save-Help
Update-Help
```

Before exploring these commands, the concept of updatable help should be discussed.

# Updatable Help
Updatable help was introduced with PowerShell 3. It gives authors the option to store the most recent versions of their help documentation outside of PowerShell on web servers.

Which modules support updatable help?A list of modules that support updatable help may be viewed by running the following command: Get-Module -ListAvailable | Where-Object HelpInfoURI -like *
Help for the core components of PowerShell is no longer a part of the Windows Management Framework package and must be downloaded before it can be viewed. The first time Get-Help is run, you will be prompted to update help.

If the previous prompt is accepted, PowerShell will attempt to download content for any module that supports updatable help.
