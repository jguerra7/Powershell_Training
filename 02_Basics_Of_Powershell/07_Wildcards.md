 Wildcards
There’s a wildcard comparison: -like and –notlike, along with the case-sensitive versions –clike and –cnotlike. These let you use common wildcard characters like * (zero or more characters) and ? (a single character) in making string comparisons:

PS C:\> 'don' -eq 'jeff'
False
PS C:\> 'don' -eq 'Don'
True
PS C:\> 'don' -ceq 'Don'
False
PS C:\> 'PowerShell'-like '*shell'
True
PS C:\> 'don' -notlike 'don*'
False
PS C:\> 'don' -like 'd?n'
True
PS C:\> 'donald' -like 'd?n'
False
These wildcards aren’t as rich as the full regular-expression language; PowerShell does support regular expressions through its –match operator, although we won’t be diving into that one in this 
