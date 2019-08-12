# Providers Performance labs

### Complete the following tasks from a PowerShell prompt:


1.  In the Registry, go to HKEY_CURRENT_USER\software\microsoft\Windows\-currentversion\explorer. Locate the Advanced key, and set its DontPrettyPath property to 1.

2.  Create a new directory called C:\Labs.

3.  Create a zero-length file named C:\Labs\Test.txt (use New-Item).

4.  Is it possible to use Set-Item to change the contents of C:\Labs\Test.txt to -TESTING? Or do you get an error? If you get an error, why?

5.  Using the Environment provider, display the value of the system environment variable %TEMP%.

6.  What are the differences between the -Filter, -Include, and -Exclude parameters of Get-ChildItem?

# Using the FileSystem Provider

In this exercise, you’ll use the FileSystem provider to create and modify directories and files. Don’t worry; we won’t operate on any of your existing content.

Prepare for this exercise by starting an elevated PowerShell session. It’s useful to see a graphical depiction of the directory/file hierarchy you’ll build, so look at Figure 8.1 for guidance. Let’s get started.

![image](https://user-images.githubusercontent.com/47218880/62884425-1dd83580-bcfc-11e9-8766-6575d24c8dec.png)

he file system hierarchy we’re building.

1. We’ll begin by setting our current working directory to the root of drive C:
```powershell
Set-Location C:\
```
2. As previously mentioned in passing, all file system objects, whether they be directory of file, are items. So, we use New-Item to build out our directories:
```powershell
PS C:\> New-Item -Name "practice" -Type Directory



    Directory: C:\



Mode                LastWriteTime     Length Name

----                -------------     ------ ----

d----        10/15/2014  10:25 AM            practice
```

Tip

You technically aren’t required to use quotation marks to enclose your object names, but I suggest doing so as a matter of practice.

We can use the –Path parameter to create the other two folders without changing our current working directory:
```powershell
New-Item –Path "C:\practice" –Name "folder1" –Type Directory

New-Item –Path "C:\practice" –Name "folder2" –Type Directory
```
3. Historically, I always use the statement dir *. to fetch a listing of only directories in a location. That won’t work in PowerShell, sadly. Instead, we need to access the PsisContainer property of the DirectoryInfo object. By the way, PsisContainer can be read as “PowerShell object that is a container.”

```powershell
Set-Location c:\practice

Get-ChildItem | Where-Object {$_.psiscontainer}



    Directory: C:\practice



Mode                LastWriteTime     Length Name

----                -------------     ------ ----

d----        10/15/2014  10:27 AM            folder1

d----        10/15/2014  10:28 AM            folder2
```
Is this making sense so far? Let’s shift our focus back to the root of C:
```powershell
Set-Location C:\
```
4. We can create new, empty files by using New-Item as well. As you doubtless observed by now, the –Type parameter is the “secret sauce” that instructs PowerShell what kind of item you’re seeking to create:
```powershell
New-Item –Name "alpha.txt" –Type File

New-Item –Path "c:\practice\folder1" –Name "beta.txt" –Type File

New-Item –Path "c:\practice\folder2" –Name "gamma.txt" –Type File
```

5. Now let’s add some data to one of the files and then read it back. We use Add-Content to, well, add new data to the file, and Get-Content to dump the contents to the console:

```powershell
PS C:\> Add-Content "alpha.txt" -Value "This is some sample data."

PS C:\> Get-Content "alpha.txt"
```
This is some sample data.

6. Time to get fancy! Let’s now use what we call a parenthetical expression to copy and paste the content of alpha.txt into gamma.txt:
```powershell
PS C:\> Add-Content "C:\practice\folder2\gamma.txt" -Value (Get-Content "C:\ alpha.txt")

PS C:\> Get-Content -Path "C:\practice\folder2\gamma.txt"

This is some sample data.
```
7. Why don’t we add some more data to alpha.txt and then pop the file open in Windows Notepad? You can see this output from my computer by examining Figure below

```powershell
Add-Content "alpha.txt" –Value "Here is more data." | notepad alpha.txt
```
![image](https://user-images.githubusercontent.com/47218880/62884733-d1d9c080-bcfc-11e9-9f4d-d3db3d29f3d6.png)

Who says that you need a word processor to author text files?

Note

We already know that PowerShell can launch (most) external executables, so it makes sense that we can start Notepad from within the PowerShell environment. It’s also cool, to me anyway, that the Add-Content cmdlet helpfully appends your new data on a new line instead of running it flush into your existing text.

8. You’ll finish this exercise by cleaning up your environment a bit. The Remove-Item command in the following example nukes the beta.txt file and forces the operation:

```powershell
Remove-Item –Path "c:\practice\folder1\beta.txt" -Force
```
What about deleting directories? Make sure to Set-Location to the root of drive C:, and we’ll delete the entire practice folder and file hierarchy. Be careful with this one! The –Recurse parameter is helpful because it moves through all subdirectories in the current path, but in the context of deletion, it’s pretty scary.

Remove-Item –Path "c:\practice" -Recurse

Note

You might recall the arithmetic order of operations from grade school that states parentheses as the highest-priority operator. In Windows PowerShell, we place the expression that we want PowerShell to process first within parentheses.

For instance, what if we have a text file containing a list of server hostnames, and we want to obtain a service listing from them all by using the –ComputerName parameter? We can use parentheses to ensure that PowerShell retrieves the server name list before passing the data as values to –Computername.

```powershell
Get-Service –Computername (Get-Content "D:\servernames.txt")
```

