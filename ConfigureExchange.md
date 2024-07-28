1) Set pagefile to 25% of total RAM
```powershell
$computersys = Get-WmiObject Win32_ComputerSystem -EnableAllPrivileges
$computersys.AutomaticManagedPagefile = $False
$computersys.Put()
$pagefile = Get-WmiObject -Query "Select * From Win32_PageFileSetting Where Name like '%pagefile.sys'"
$pagefile.InitialSize = <New_Value_For_Size_In_MB>
$pagefile.MaximumSize = <New_Value_For_Size_In_MB>
$pagefile.Put()
```
2) Rename database
```powershell
Get-MailboxDatabase
Set-MailboxDatabase "<DB Name>" -Name "<new name>"
```
3) Move database to another location
Mount new Disk (mount folder preferred)
```powershell
Get-MailboxDatabase | Format-List Name, EdbFilePath, LogFolderPath
Move-DatabasePath "<db name>" -EdbFilePath "<path to db location>\<db name>.edb" -LogFolderPath "<path to db location>"
```
4) Enable circular logging
```powershell
Get-MailboxDatabase "<db name>" | Format-Table Name, CircularLoggingEnabled
Set-MailboxDatabase "<db name>" -CircularLoggingEnabled $True
Dismount-Database "<db name>" -Confirm:$False
Get-MailboxDatabase "<db name>" -Status | Format-Table Name, Mounted
Mount-Database "<db name>" -Confirm:$False
Get-MailboxDatabase "<db name>" -Status | Format-Table Name, Mounted
Test-MAPIConnectivity
```
