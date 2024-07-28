# Exchange Mailbox server 
### Prerequisites:
1) Windows components
```powershell
Install-WindowsFeature Server-Media-Foundation, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
```
2) [.NET Framework 4.8](https://download.visualstudio.microsoft.com/download/pr/014120d7-d689-4305-befd-3cb711108212/0fd66638cde16859462a6243a4629a50/ndp48-x86-x64-allos-enu.exe)
3) [Visual C++ for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679)
4) [Visual C++ for Visual Studio 2013](https://support.microsoft.com/help/4032938/update-for-visual-c-2013-redistributable-package)
5) [Unified Communications Managed API 4.0 Runtime](https://www.microsoft.com/download/details.aspx?id=34992)
6) [IIS URL Rewrite Module](https://www.iis.net/downloads/microsoft/url-rewrite)


### Installing:
1) Mount ISO with Exchange Server installation files
2) Go to mounted drive
3) Run Powershell as admin
4) Install Mailbox Role 
```powershell
.\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /mode:Install /r:MB
```
