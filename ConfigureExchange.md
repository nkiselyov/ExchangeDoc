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
5) Change Internal and External URL
```powershell
$subdomain = "mail" #enter subdomain
$domain = "smfrv.ru" #enter domain
$servername = "exch1" #enter server name

Get-ClientAccessServer -Identity $servername | Set-ClientAccessServer -AutoDiscoverServiceInternalUri "https://autodiscover.$domain/Autodiscover/Autodiscover.xml"
Get-EcpVirtualDirectory -Server $servername | Set-EcpVirtualDirectory -ExternalUrl "https://$subdomain.$domain/ecp" -InternalUrl "https://$subdomain.$domain/ecp"
Get-WebServicesVirtualDirectory -Server $servername | Set-WebServicesVirtualDirectory -ExternalUrl "https://$subdomain.$domain/EWS/Exchange.asmx" -InternalUrl "https://$subdomain.$domain/EWS/Exchange.asmx"
Get-MapiVirtualDirectory -Server $servername | Set-MapiVirtualDirectory -ExternalUrl "https://$subdomain.$domain/mapi" -InternalUrl "https://$subdomain.$domain/mapi"
Get-ActiveSyncVirtualDirectory -Server $servername | Set-ActiveSyncVirtualDirectory -ExternalUrl "https://$subdomain.$domain/Microsoft-Server-ActiveSync" -InternalUrl "https://$subdomain.$domain/Microsoft-Server-ActiveSync"
Get-OabVirtualDirectory -Server $servername | Set-OabVirtualDirectory -ExternalUrl "https://$subdomain.$domain/OAB" -InternalUrl "https://$subdomain.$domain/OAB"
Get-OwaVirtualDirectory -Server $servername | Set-OwaVirtualDirectory -ExternalUrl "https://$subdomain.$domain/owa" -InternalUrl "https://$subdomain.$domain/owa"
Get-PowerShellVirtualDirectory -Server $servername | Set-PowerShellVirtualDirectory -ExternalUrl "https://$subdomain.$domain/powershell" -InternalUrl "https://$subdomain.$domain/powershell"
Get-OutlookAnywhere -Server $servername | Set-OutlookAnywhere -ExternalHostname "$subdomain.$domain" -InternalHostname "$subdomain.$domain" -ExternalClientsRequireSsl $true -InternalClientsRequireSsl $true -DefaultAuthenticationMethod NTLM
```
