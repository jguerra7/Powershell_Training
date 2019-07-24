# What is a module?
Modules were introduced with the release of PowerShell version 2.0. Modules represented a significant step forward over snap-ins. Unlike snap-ins, modules do not have to be formally installed or registered for use with PowerShell.

It is most common to find a module that targets a specific system or focuses on a small set of related operations. For example, the Microsoft.PowerShell.LocalAccounts module contains commands for interacting with the local account database (users and groups).

> A module may be binary, script, dynamic, or manifest:
```
- Binary module: This is written in a language, such as C# or VB.NET, 
and then compiled into a library (DLL)
- Script module: This is a collection of functions written in the PowerShell language. 
The commands typically reside in a script module file (PSM1)
- Dynamic module: This does not have files associated with it. 
This is created using the New-Module command. The following command creates a very simple dynamic module 
that adds the Get-Number command:
```
```powershell
New-Module -Name TestModule -ScriptBlock { 
    function Get-Number { return 1 } 
} 
```
A manifest module combines different items to make a single consistent module. For example, a manifest may be used to create a single module out of a DLL containing cmdlets and a script containing functions. For example, Microsoft.PowerShell.Utility is a manifest module that combines a binary and script module.

A manifest module may also be used to build commands based on WMI classes. The cmdlets-over-objects feature was added with PowerShell 3, an XML file with a cdxml extension (Cmdlet definition XML). For example, the Defender module creates commands based on WMI classes in ROOT/Microsoft/Windows/Defender namespace.

The manifest module file serves a number of purposes, as follows:
```
- Describing the files that should be loaded (such as a script module file, a binary library, 
nd a cmdlet definition XML file)
- Listing any dependencies the module may have (such as other modules, 
.NET libraries, or other DLL files)
- Listing the commands that should be exported (made available to the end user)
Recording information about the author or the project
```
When loading a module with a manifest, PowerShell will try and load any listed dependencies. If a module fails to load because of a dependency, the commands written as part of the module will not be imported.
