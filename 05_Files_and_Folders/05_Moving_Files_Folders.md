**Move-Item** cmdlet is used to move a directory by passing the path of the directory to be moved and destination path where the folder is to be moved.


In this example, we'll move a folder D:\Temp\Test to D:\Temp\Test1

> Type the following command in PowerShell ISE Console
```powershell

Move-Item D:\temp\Test D:\temp\Test1

```
You can see the Test directory moved to Test1 directory in Windows Explorer.

In this example, Create a file test.txt in Test folder in D:\Temp\ and then run the same command.

> Type the following command in PowerShell ISE Console
```powershell
Move-Item D:\temp\Test D:\temp\Test1
```
You can see the content of Test1 directory in Windows Explorer where it contains both the Test directory and test file.
