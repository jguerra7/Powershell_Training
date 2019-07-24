# Create a Folder

**New-Item** cmdlet is used to create a directory by passing the path using -Path as path of the directory and -ItemType as Directory.


In this example, we'll create a folder in D:\Temp\ with name "Test Folder"

Type the following command in PowerShell ISE Console
```powershell
New-Item -Path 'D:\temp\Test Folder' -ItemType Directory

```
Output
You will see the following output.
```
Directory: D:\temp

Mode                LastWriteTime     Length Name                                               
----                -------------     ------ ----                                               
d----          4/3/2018   7:06 PM            Test Folder   
```
You can see the same in Windows Explorer where Test Folder is created in D:/temp folder.
