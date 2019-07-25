# Cmdlet to use 

Copy-Item cmdlet is used to copy a directory by passing the path of the directory to be copied and destination path where the folder is to be copied.


In this example, we'll copy a folder D:\Temp\Test Folder as D:\Temp\Test Folder1

> Type the following command in PowerShell ISE Console
```powershell
Copy-Item 'D:\temp\Test Folder' 'D:\temp\Test Folder1'
```
You can see the Test Folder1 in Windows Explorer created.

In this example, we'll copy a folder recursively D:\Temp\Test Folder to D:\Temp\Test Folder1

> Type the following command in PowerShell ISE Console
```powershell
Copy-Item 'D:\temp\Test Folder' -Destination 'D:\temp\Test Folder1'
```
You can see the content of Test Folder1 in Windows Explorer where it contains both the Test Folder and test file.
