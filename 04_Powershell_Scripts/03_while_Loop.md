
In the DemoWhileLessThan.ps1 script, you use the expanding string to print the status message of the value of the $i variable during each trip through the While loop. You suppress the expanding nature of the expanding string for the first $i variable so you can tell which variable you are talking about. As soon as you have done this, you increment the value of the $i variable by one. To do this, you use the $i++ syntax. This is identical to saying the following.
```
$i = $i + 1
```
The advantage is that the $i++ syntax requires less typing. The DemoWhileLessThan.ps1 script is shown here.

> DemoWhileLessThan.ps1

```powershell
$i = 0
While ($i -lt 5)
 {
  "`$i equals $i. This is less than  5"
  $i++
 } #end while $i lt 5
 ```
 When you run the DemoWhileLessThan.ps1 script, you receive the following output.
 
 ```powershell
 $i equals 0. This is less than  5
$i equals 1. This is less than  5
$i equals 2. This is less than  5
$i equals 3. This is less than  5
$i equals 4. This is less than  5
PS C:\>
```
