# Powershell or CMD

Is Powershell just the command line prompt with a blue background

## Powershell and cmd.exe similarities
  - Both provide a command-line environment
  - Both allow the creation of scripts
  -The old 'trustees" in the Cmd.exe (commands) still work in Powershell
    -Dir
    -Cls
    -Etc.
    
## So What's the difference between Powershell and Cmd.exe?

  - Cmd.exe provided a command-line interface for a very limited set of functionality
  - Cmd.exe is a text-based scripting environment
    -Makes dealing with command results difficult
  - Cmd.exe does not provide access to amny aspects of the OS and Applications
  - Powershell is an object-based scripting language
    -Everythin is an object
    -Makes dealing with command results very easy and efficient
  - Powershell provides access to the .NET Framework, the building blocks of Windows functionalities.

## Powershell commands

Starting at the beginning, here’s the traditional “Hello world” program in PowerShell:

```powershell
'hello world'
```
But “Hello world” itself isn’t interesting. Here’s something a bit more complicated:
```powershell
Get-ChildItem -Path $env:windir\*.log |
Select-String -List error |
Format-Table Path,LineNumber –AutoSize
```
Although this is more complex, you can probably still figure out what it does. It searches all the log files in the Windows directory, looking for the string “error”, and then prints the full name of the matching file and the matching line number. “Useful, but not special,” you might think, because you can easily do this using cmd.exe on Windows or bash on UNIX. What about the “big, really big” thing? Well, how about this example:
```powershell
([xml] [System.Net.WebClient]::new().
    DownloadString('http://blogs.msdn.com/powershell/rss.aspx')).
        RSS.Channel.Item |
            Format-Table title,link
```
Now we’re getting somewhere. This script downloads the RSS feed from the PowerShell team blog and then displays the title and a link for each blog entry. By the way, you weren’t expected to figure out this example yet. If you did, you can move to the head of the class!



> Typical Command Example:
![image](https://user-images.githubusercontent.com/47218880/61650708-e258c700-ac79-11e9-9ff8-8521ec686382.png)

> Powershell Command Example:
![image](https://user-images.githubusercontent.com/47218880/61650874-52ffe380-ac7a-11e9-8d52-9f9f5c7274c3.png)

![image](https://user-images.githubusercontent.com/47218880/61651077-b9850180-ac7a-11e9-9148-fe7500f712fc.png)

## So What's the difference between Powershell and Cmd.exe?
  - Powershell provides the programming power and accessibility of an object oriented programming language in a scripting environment.
  
