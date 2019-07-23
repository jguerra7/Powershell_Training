
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
