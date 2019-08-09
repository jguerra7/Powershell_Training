# Creating a Powershell Profile

Simple Scripting Lab to setup your powershell profile

1. Open up powershell 
  a. At the bottom of the screen, in the "Type here to search" textfield. Type in **powershell** and open up the "Windows Powershell app"
2. Once the Powershell prompt is up type in: 
```powershell
New-Item  -path $profile -type file -force
```
and press **enter**.
3. Once that is executed, go back to the bottom of the screen and in "Type here to search" textfield. Type in **File Explorer** and open up and navigate to the file location specified in the powershell prompt after you executed the above command. The path that has the folder you are looking for is listed in the : 
```powershell
  Directory: your file path will be show here
  ```
go to the directory path of the profile location and open up the "Windows Powershell" folder 
and open up the ".ps1" file ( It will be blank)
4. Once the ".ps1" file is open, Type in this cmdlet script to the file and save.
```powershell
# Display Greeting

Clear-Host
Write-Host "`t `t `t --------------------------------ATTENTION!----------------------------------------"
Write-Host "`t `t This computer is only for UNCLASSIFIED use by Authorized CyberTraining USAF Personnel"
Write-Host " "
Write-Host " "

```
5. Now make sure powershell is closed and relaunch powershell. You should see the text you typed in the ".ps1" file from the "windows powershell" folder.


