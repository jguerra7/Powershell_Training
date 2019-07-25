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

Move-Item cmdlet is used to move a file by passing the path of the file to be moved and destination path where the file is to be moved.

Examle 1
In this example, we'll move a folder D:\Temp\Test\Test.txt to D:\Temp\Test1

> Type the following command in PowerShell ISE Console
```powershell
Move-Item D:\temp\Test\Test.txt D:\temp\Test1
```
You can see the Test.txt in Test1 directory now. Test.txt has been moved from Test to Test1.
