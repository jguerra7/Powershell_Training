# Creating a Powershell Profile

Simple Scripting Lab to setup your powershell profile

1. Open up powershell 
2. Once the Powershell prompt is up type in: 
```powershell
New-Item  -path $profile -type file -force
```
3. Now go to the directory path of the profile location and open up the "Windows Powershell" folder 
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


