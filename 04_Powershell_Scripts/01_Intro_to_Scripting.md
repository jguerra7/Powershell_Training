
# Scripts
Now that we have learned some useful commands, it would be nice to be able to record a sequence of commands, so that we can execute them all at once. In this chapter, we will learn how to accomplish this with scripts. We will also cover the following topics:
```
Execution policies
Adding parameters to scripts
Control structures
Profiles
```
## Packaging commands
Saving commands in a file for reuse is a pretty simple idea. In PowerShell, the simplest kind of these files is called a script and it uses the .ps1 extension, no matter what version of PowerShell you're using. For example, if you wanted to create a new folder, under c:\temp, with the current date as the name and then change to that folder, you could put these commands in a file:

Note that I'm using the top portion of the ISE to edit the file contents and I have saved the file as dateFolder.ps1 in the c:\temp folder. To run the script, you can simply type the name of the file at prompt as follows

![image](https://user-images.githubusercontent.com/47218880/61737423-ccb4d180-ad4d-11e9-9e79-dcfa0803c1bc.png)

f you have the file loaded in the ISE, you can also use the Run button on the toolbar to run the current file.

It's possible that when you try to run this script, you will receive an error complaining about the execution policy, instead of seeing the current path being set to a new folder. To understand why this would have happened, we need to discuss the concept of execution policies.


# Execution policy
Execution policy is a safety feature in PowerShell that enables the system to control which scripts are able to be run. I say safety instead of security because execution policy is trivial to circumvent. Execution policy are more like the safety of a gun, which prevents accidental discharge of the weapon. An execution policy is an attempt to prevent users from accidentally executing scripts.

Possible execution policy values include the following:
```
Restricted
AllSigned
RemoteSigned
Unrestricted
```
The Restricted setting means that the scripts cannot be run at all. AllSigned means that all scripts must be digitally signed to run. Unrestricted says that any script will run. RemoteSigned is a middle-ground setting that says that any local scripts will run, but scripts from remote sources (like the Internet or untrusted UNC paths) need to be digitally signed.

Prior to Windows Server 2012R2, the default execution policy for all systems was Restricted, meaning that by default scripts were not allowed to run at all. With Server 2012R2, the default was changed to RemoteSigned.

Attempting to run a script when the execution policy does not permit it, results in an error such as the following:

![image](https://user-images.githubusercontent.com/47218880/61737580-21f0e300-ad4e-11e9-8445-5294c7f9ba7a.png)

To see what your current execution policy is set to, use the Get-ExecutionPolicy cmdlet. To set the execution policy, you would use the Set-ExecutionPolicy cmdlet.

```
### TIP
*Important!*

Since the execution policy is a system setting, changing it requires you to run an elevated session. 
Attempting to change the execution policy from a user session, will result in an "Access Denied" error writing to the registry.

```
The following figure shows the results of running the script after the execution policy has been set to an appropriate level:

![image](https://user-images.githubusercontent.com/47218880/61737674-549adb80-ad4e-11e9-8d10-9a061cd25e24.png)

In my experience, the RemoteSigned setting is most practical. However, in a secure environment such as a production data center, I can easily see that using an AllSigned policy could make sense.

























