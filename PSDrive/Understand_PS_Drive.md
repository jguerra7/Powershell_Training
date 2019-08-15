# WHAT ARE PROVIDERS?
In Windows PowerShell nomenclature, we can look at a provider as an adapter that gives us access to a particular data store. For instance, once you buy a compatible Universal Serial Bus (USB) cable and plug one end into a portable hard drive and the other into a USB port on your computer, you have access to all the resources on that external disk drive.

Likewise, Windows PowerShell ships with the following default PSProviders, as they’re called:
```powershell
PS C:\> Get-PSProvider | Select-Object -Property name, drives



Name                                    Drives

----                                    ------

Alias                                   {Alias}

Environment                             {Env}

FileSystem                              {C, E, D}

Function                                {Function}

Registry                                {HKLM, HKCU}

Variable                                {Variable}

WSMan                                   {WSMan}
```
The WSMan provider appears in the Get-PSProvider output only if you’ve enabled PowerShell remoting; you’ll learn how to do that later on in the book. Also, you may wonder why I used the Select-Object clause; after all, the output only has three properties.

My answer, quite honestly, is that I want to expose only the properties that directly relate to what we’re learning. Why not take advantage of filtering whenever possible?
# Functions Provided by a Provider
The PSProvider makes a particular data store available to you, the PowerShell user. For example, the Alias provider stores all the aliases that are defined on the local system.

The Environment provider encompasses all environment variables, the FileSystem provider opens up the file system to us, and so forth.

Although we have this collection of seven built-in PowerShell providers, that doesn’t mean that these are all there are—not by a long shot.

Some Windows features and external applications bring along new PSProviders; two that come to mind are the Active Directory Domain Services (AD DS) server feature and the SQL Server relational database management system (RDBMS).

In fact, take a look at this screenshot that shows Get-PSProvider output on a Windows Server 2012 domain controller that also hosts a SQL Server 2012 instance:
```powershell
PS C:\> Get-PSProvider



Name                 Capabilities                       Drives

----                 ------------                       ------

Alias                ShouldProcess                      {Alias}

Environment          ShouldProcess                      {Env}

FileSystem           Filter, ShouldProcess, Credentials {C, A, D, Z}

Function             ShouldProcess                      {Function}

Registry             ShouldProcess, Transactions        {HKLM, HKCU}

Variable             ShouldProcess                      {Variable}

SqlServer            Credentials                        {SQLSERVER}

ActiveDirectory      Include, Exclude, Filter, Shoul... {AD}
```
In the previous output, notice the Capabilities property. As it happens, different PSProviders offer different, well, capabilities. To wit:

Image ShouldProcess: The provider supports the –Confirm and –WhatIf parameters.

Image Credentials: The provider supports the use alternate credentials at runtime.

Image Transactions: The provider supports atomic transactions, where one or more PowerShell statements succeed or fail together.

Image Filter, Include, Exclude: The provider enables you to granularly manipulate the provider’s content.

As you might think, the SQL Server PSProvider allows us to tap into any database in the local SQL Server instance (assuming that our user account has permissions, of course). The same goes for the Active Directory PSProvider.

What’s important to understand is that PSProviders aren’t directly accessible to us. Instead, PSProviders are used through a related technology known as the PSDrive.

# INTRODUCTION TO DEFAULT PSDRIVES
You probably noticed the Drives property in the Get-PSProvider output. This data represents the entry point into that particular data store. We can use either the Set-Location cmdlet or its more common cd alias to switch our context from the default provider (FileSystem) to, say, the Variable PSProvider. Check out this partial output from my Windows 8.1 system:
```powershell
PS C:\> Set-Location Variable:

PS Variable:\> dir



Name                           Value

----                           -----

$                              Variable:

?                              True

^                              Set-Location

args                           {}

buffer                         80,5000

ConfirmPreference              High

console                        System.Management.Automation.Internal.Host.In...

ConsoleFileName

DebugPreference                SilentlyContinue

Error                          {The term 'dird' is not recognized as the nam...

ErrorActionPreference          Continue

ErrorView                      NormalView

ExecutionContext               System.Management.Automation.EngineIntrinsics

false                          False

FormatEnumerationLimit         4

HOME                           C:\Users\Tim

Host                           System.Management.Automation.Internal.Host.In...

input                          System.Collections.ArrayList+ArrayListEnumera...

LASTEXITCODE                   0

MaximumAliasCount              4096
```
We don’t need to concern ourselves specifically with what these variables mean; we have plenty of time for that when we delve into Windows PowerShell scripting later on in the book. For now, I just want you to get comfortable with navigating among the different providers.

We can use Get-PSDrive to obtain a listing of available PSDrives on our computer:
```powershell
PS C:\> Get-PSDrive



Name           Used (GB)     Free (GB) Provider      Root

----           ---------     --------- --------      ----

Alias                                  Alias

C                 123.37        109.17 FileSystem    C:\

Cert                                   Certificate   \

D                                      FileSystem    D:\

E                 334.51       1528.48 FileSystem    E:\

Env                                    Environment

Function                               Function

HKCU                                   Registry      HKEY_CURRENT_USER

HKLM                                   Registry      HKEY_LOCAL_MACHINE

Variable                               Variable

WSMan                                  WSMan
```
You’ll observe that some PSProviders (namely FileSystem and Registry) offer more than one PSDrive.

# A Familiar Navigation System
Notice that we specify a colon (:) when we change context to a PSDrive. Remember that the concept of drives is intentional with all its metaphorical baggage. In other words, we browse PSDrives using the standard Cmd.exe navigation commands we’ve always used.

Dir, you’ll recall, is just an alias for Get-ChildItem. Linux aficionados can use ls if they want. In point of fact, check out the following partial output where we get a list of all system aliases (alii?) while working in the context of the Variable PSDrive:
```powershell
PS Variable:\> ls alias:



CommandType     Name

-----------     ----

Alias           % -> ForEach-Object

Alias           ? -> Where-Object

Alias           ac -> Add-Content

Alias           asnp -> Add-PSSnapin

Alias           cat -> Get-Content

Alias           cd -> Set-Location

Alias           chdir -> Set-Location

Alias           clc -> Clear-Content

Alias           clear -> Clear-Host

Alias           clhy -> Clear-History

Alias           cli -> Clear-Item

Alias           clp -> Clear-ItemProperty

Alias           cls -> Clear-Host
```
Thus, if we want to return our focus to the file system, no problem; just use cd or Set-Location to switch to that PSDrive:
```powershell
PS Variable:\>cd c:
```
```
Tip

Some PowerShell users employ the sl alias for Set-Location, by the way. So many options to choose from!
```

The FileSystem provider is a bit different from some of the other PSProviders inasmuch as it includes a separate PSDrive for each mounted volume on your system. We’ll delve more into that point in a moment.

```powershell
PS Variable:\> cd c:

PS C:\> dir



    Directory: C:\



Mode                LastWriteTime     Length Name

----                -------------     ------ ----

d----         4/22/2014   7:57 PM            Intel

d----         8/22/2013  10:22 AM            PerfLogs

d-r--        10/13/2014   1:03 PM            Program Files

d-r--        10/13/2014   1:10 PM            Program Files (x86)

d-r--         4/30/2014   1:18 PM            Sandbox

d----         7/21/2014  11:08 AM            savedhelp

d----         9/29/2014  11:49 AM            temp

d-r--          9/2/2014   8:36 AM            Users

d----        10/13/2014  12:23 PM            Windows
```
## What’s an Item?
Thus far, you see that these PSDrives were designed to give you the comfort of navigating different data stores in a familiar way by using Linux- or Windows-like shell commands (actually aliases to PowerShell cmdlets, as you know).

Once you start delving into PSDrives, you’ll come across the word item all the time in cmdlet listings:
```powershell
PS C:\> Get-Command -Noun *item* | Where-Object {$_.CommandType -eq "cmdlet"}



CommandType     Name                                               Source

-----------     ----                                               ------

Cmdlet          Clear-Item                                         Microsoft...

Cmdlet          Clear-ItemProperty                                 Microsoft...

Cmdlet          Copy-Item                                          Microsoft...

Cmdlet          Copy-ItemProperty                                  Microsoft...

Cmdlet          Get-ChildItem                                      Microsoft...

Cmdlet          Get-ControlPanelItem                               Microsoft...

Cmdlet          Get-Item                                           Microsoft...

Cmdlet          Get-ItemProperty                                   Microsoft...

Cmdlet          Get-ItemPropertyValue                              Microsoft...

Cmdlet          Invoke-Item                                        Microsoft...

Cmdlet          Move-Item                                          Microsoft...

Cmdlet          Move-ItemProperty                                  Microsoft...

Cmdlet          New-Item                                           Microsoft...

Cmdlet          New-ItemProperty                                   Microsoft...

Cmdlet          Remove-Item                                        Microsoft...

Cmdlet          Remove-ItemProperty                                Microsoft...

Cmdlet          Rename-Item                                        Microsoft...

Cmdlet          Rename-ItemProperty                                Microsoft...

Cmdlet          Set-Item                                           Microsoft...

Cmdlet          Set-ItemProperty                                   Microsoft...

Cmdlet          Show-ControlPanelItem                              Microsoft...
```
In PSProvider nomenclature, everything is an “item,” whether we are talking about a variable, a directory, a file, or a Registry value. Once again, the PowerShell team strives to give us a standardized, unified interface for working with different data stores.
```
Note: Help! I’m in Alias Overload

In this hour, I’ve tried (perhaps to the point of overkill) to stress that we can access and use these PSDrives by using aliases that map to well-loved shell commands (dir, ls, cd, type, cat, and the like).

However, for the duration of this hour, I’ll instead use the underlying commands instead of the aliases, with some exception. I need you to never forget that when you use aliases that “look and feel” like their Linux or DOS counterparts, you are actually running PowerShell commands under the hood.
```
Okay, then. I’m confident that you have a basic understanding of what PSProviders and PSDrives are. It’s now time to learn how to leverage these data stores to accomplish meaningful work with Windows PowerShell. We’ll start with the FileSystem provider, the use of which should already be familiar to you.

## USING THE FILESYSTEM PROVIDER
We’ll start with the FileSystem provider because, frankly, you are connected to this provider by default every time you start a Windows PowerShell session.

To start, let’s view all the PSDrives that are associated with your system’s FileSystem PSProvider. Remember that your output may not match mine:
```powershell
PS C:\> Get-PSDrive -PSProvider FileSystem



Name           Used (GB)     Free (GB) Provider      Root

----           ---------     --------- --------      ----

C                 124.49        108.05 FileSystem    C:\

D                                      FileSystem    D:\

E                 334.51       1528.47 FileSystem    E:\
```
On my Windows 8.1 computer, I have three PSDrives that (not coincidentally) map to the three volumes that are attached to the system.

Under the hood, those three mount points (C:, D:, and E:) actually correspond to functions. Look at the following partial output:

```powershell
PS C:\> Set-Location Function:

PS Function:\> Get-ChildItem



CommandType     Name

-----------     ----

Function        A:

Function        B:

Function        C:

Function        cd..

Function        cd\

Function        Clear-Host

Function        D:

Function        E:
```
Pretty cool, isn’t it? In the name of improving your efficiency with the shell, you can also make use of the –Path parameter of Get-ChildItem to recast the previous example:
```powershell
Get-ChildItem –Path Function:
```
By now you are well aware that the PowerShell team uses function definitions and other “smoke and mirror” techniques to make PowerShell as intuitive as possible for users.

One more thing: you need to understand that although PSProviders all do the same basic thing (exposing different datastores as if they are filesystems), each PSProvider has its own capability. The FileSystem provider, for instance, has –File and –Directory parameters that aren’t supported by, say, the Function: provider.

Long story short, you’ll need to experiment as you work with different PSProviders to see what’s possible in each respective context.











