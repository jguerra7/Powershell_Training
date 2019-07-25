 # Creating a Scheduled PowerShell Job

In this scenario, you’ll create a scheduled Windows PowerShell job that gathers the 10 most recent error messages from the local host’s System event log. We’ll have the job occur every Monday, Wednesday, and Friday evening at 7 p.m.

1. You can, and probably should, run the following commands to delete all the background and scheduled jobs from our local system:
```powershell
Get-Job | Remove-Job

Unregister-ScheduledJob *
```
You can also run the aforementioned commands after you complete this exercise to reset your local system to prehour defaults.

2. It’s time to define our trigger. Remember that our trigger condition is Mon-Wed-Fri at 7 p.m. You’ll see that we make use of some new parameters of the New-JobTrigger cmdlet, and that we specify time in 24-hour format to avoid ambiguity:

```powershell

$trig = New-JobTrigger –Weekly –DaysOfWeek Monday, Wednesday, Friday –At "19:00" –WeeksInterval 1
```
3. Now we’ll create a set of scheduled job options that (1) hides the job from the Windows Task Scheduler interface; and (2) ensures that the system has been idle for at least 10 minutes in order to activate the trigger:

```powershell

$opt = New-ScheduledJobOption –HideInTaskScheduler –IdleDuration 00:15:00
```
4. Next, let’s define the scheduled job:

```powershell

PS C:\> Register-ScheduledJob -Name NightlyErrors -ScriptBlock {Get-EventLog -LogName system -EntryType Error | Select-Object -First 10 -Property TimeGenerated,EventID, message | Format-List} -ScheduledJobOption $opt
```
5. Nuts! We forgot to add our trigger object! No problem; there’s a cmdlet for that. We can retroactively add options or triggers to an existing scheduled job.

First, we pull the NightlyErrors job into our session:

```powershell
PS C:\> Get-Scheduledjob -Name NightlyErrors



Id         Name            JobTriggers     Command

--         ----            -----------     -------

4          NightlyErrors   0               get-eventlog -LogName system-Ent...
```
Second, we can use the pipeline and Set-ScheduledJob to modify the existing job definition, adding in the $trig trigger object as a parameter value:

```powershell
PS C:\> Get-ScheduledJob -Name NightlyErrors | Set-ScheduledJob -Trigger $trig

PS C:\> Get-Scheduledjob -Name NightlyErrors



Id         Name            JobTriggers     Command

--         ----            -----------     -------

4          NightlyErrors   1               get-eventlog -LogName system-Ent...


```
Sweet! Looks pretty good thus far.

6. Let’s pack our new NightlyErrors job into a variable and then force-run it once or twice:

```powershell

$ne = Get-ScheduledJob –Name NightlyErrors

$ne.StartJob()
```
7. Just for grins, I want you to inspect the members of our scheduled job object in order to familiarize yourself with what’s possible with this object:
```powershell
$ne | Get-Member
```
8. Now that we know our scheduled job has result data, we can retrieve child job metadata and ultimately the output itself:

```powershell
PS C:\> Get-Job -Name NightlyErrors -IncludeChildJob



Id     Name            PSJobTypeName   State         HasMoreData     Location

--     ----            -------------   -----         -----------     --------

8      NightlyErrors   PSScheduledJob  Completed     True            localhost

10     Job10                           Completed     True            localhost



PS C:\> Receive-Job -Id 8



TimeGenerated : 11/7/2014 1:18:13 PM

EventID       : 7001

Message       : The Computer Browser service depends on the Server service

                which failed to start because of the following error:

                %%1058



TimeGenerated : 11/7/2014 1:18:13 PM

EventID       : 7001

Message       : The Computer Browser service depends on the Server service

                which failed to start because of the following error:

                %%1058
```
When you’re finished, don’t forget to remove your new job object (unless you really want to use it, that is). For instance, you could try the following one-liner to remove all jobs with a HasMoreData value of False:

```powershell
Get-Job | Where-Object { -not $_.HasMoreData } | Remove-Job
```
SUMMARY
You now understand how to get Windows PowerShell multitasking and how to free up your session prompt whenever you need it. There’s a lot to the Windows PowerShell job subsystem, that’s for sure.
