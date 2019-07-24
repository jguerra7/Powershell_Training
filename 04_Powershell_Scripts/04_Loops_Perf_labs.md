# Loops performance Labs
> Type these programming scripts into files and run them and manipulate them to see what they do.

## Foreach

ForEach has two different meanings in PowerShell. One is a keyword and the other is an alias for the ForEach-
Object cmdlet. The former is described here.

This example demonstrates printing all items in an array to the console host:
```powershell
$Names = @('Amy', 'Bob', 'Celine', 'David')
ForEach ($Name in $Names)
{
Write-Host "Hi, my name is $Name!"
}
```
This example demonstrates capturing the output of a ForEach loop:
```powershell
$Numbers = ForEach ($Number in 1..20) {
$Number # Alternatively, Write-Output $Number
}
```
Like the last example, this example, instead, demonstrates creating an array prior to storing the loop:
```powershell
$Numbers = @()
ForEach ($Number in 1..20)
{
$Numbers += $Number
}
```
## For
The for statement runs a statement list zero or more times based on an initial setting, a conditional test, and a repeated statement, most often used with numeric counters.

```powershell
for($i = 0; $i -lt 3; $i++)
{
    Write-Output $i
}
```

> For loops are often nested to repeat actions, such as for rows and columns. For example:
```powershell
for($i = 0; $i -lt 3; $i++)
{
    $line = ''
    for($j = 0; $j -lt 3; $j++)
    {
        $line += $i.ToString() + $j.ToString() + '  '
    }
    Write-Output $line
}
```
## Continue and Break decision Structures















