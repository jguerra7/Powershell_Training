```powershell
function Get-BatteryStatus {
    <#
    .SYNOPSIS
    Retrieve battery information

    .DESCRIPTION
    Retrieve battery information

    .EXAMPLE
    Get-BatteryStatus

    .NOTES
      Training
    #>
    PARAM()
    try {
        Add-Type -Assembly System.Windows.Forms
        [System.Windows.Forms.SystemInformation]::PowerStatus
    } catch {
        $PSCmdlet.ThrowTerminatingError($_)
    }
}
```
