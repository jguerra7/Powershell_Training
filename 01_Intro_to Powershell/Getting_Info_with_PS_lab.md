# Getting Event Log Information with Windows PowerShell

In this exercise, you’ll dive into learning Windows PowerShell by firing up a console session and using the Get-Eventlog cmdlet. Don’t be intimidated by the sometimes strange syntax we’ll see. Everything will be fully explained to you in time, and before long it will all be second nature to you anyway.

So for now just sit back, type code, review the output, and enjoy the ride without worrying about the fine syntax details. More will be revealed, I promise!

By the way, the code we use in this Try It Yourself exercise works in any version of Windows PowerShell, so feel free to work through the following steps on your Windows server or client computer. Enjoy!

1. Open an elevated command prompt. The specific method for doing this varies a bit depending upon your operating system. The general instructions on Windows client systems are to (a) press the Windows key on your keyboard; (b) type cmd and press Enter; (c) right-click the resulting Cmd.exe icon; and (d) select Run as Administrator from the shortcut menu.

2. Now that you are in an administrative Cmd.exe session, you can start Windows PowerShell by typing powershell and pressing Enter. By the way, it’s implied that you should press Enter after every command from now on, okay?

The reason why I’m having you enter Windows PowerShell from the Windows command prompt is simply to remind you that it can be done this way. Having options is great, right?

You can tell that you’re in a Windows PowerShell session because the command prompt is prepended with (appropriately enough) PS.

3. Okay, let’s get down to business. We’ll start by viewing all the event logs on our system. We do this with the Get-EventLog cmdlet along with the list parameter:
```powershell
Get-EventLog -list
```
Although I show you cmdlets in title case, it’s important for you to know that cmdlets are not case sensitive. Therefore, you can get the same result by typing GET-EVENTLOG, get-eventlog, or GeT-eVeNtLoG. The Get-EventLog-list statement gives us a tabular view of all event logs on our system, along with some pertinent metadata like their maximum log file size and the number of entries contained therein.

4. If you want to view the entries in a specific log, such as the Application log, we can issue the following statement:
```powershell
Get-EventLog –LogName Application
```
5. Whoa! The previous command gave us a lot of information, wouldn’t you agree? Let’s try viewing only the most recent five entries, shall we? Try this:
```powershell
Get-EventLog –LogName Application –Newest 5
```
6. That’s a little better, right? However, the tabular view is a bit cramped onscreen. Why don’t we format the output in a more eye-friendly way onscreen:

Figure below shows the difference in output. That strange vertical bar character you used is called the pipe. You can access the pipe character by holding Shift and typing the key above Enter on your keyboard. We use pipe a lot in Windows PowerShell to chain commands together.

![image](https://user-images.githubusercontent.com/47218880/62873494-1eb19d00-bce5-11e9-8004-d7d2e93f04b3.png)
You can view Windows PowerShell output in several different ways.

7. To save yourself some typing, press the up-arrow key on your keyboard; notice that this allows you to access previously typed commands.

Let’s assume that you want a printed record of this Application event log output. To do that, you can add a third link to your Windows PowerShell pipe chain:
```powershell
Get-EventLog –LogName Application –Newest 5 | Format-List | Out-File "C:\ events.txt"
```
8. Finally, you can open your newly created text log file in Notepad directly from our Windows PowerShell session:
```powershell
Notepad C:\events.txt
```
9. To exit your Windows PowerShell session and return to Cmd.exe, type exit. Type exit a second time to close the Cmd.exe command window. You’re done!
