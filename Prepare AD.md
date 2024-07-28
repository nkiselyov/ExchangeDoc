### Prerequisites:
1) Installed RSAT-ADDS
   ```powershell
   Install-WindowsFeature RSAT-ADDS
   ```
2) Member of Enterprise Admins and Schema Admins
3) Machine in same site as Schema Master

### Steps:
1) Mount ISO with Exchange Server installation files
2) Go to mounted drive
3) Run Powershell as admin
4) Prepare Schema:
```powershell
.\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /PrepareSchema
```
5) Prepare Active Directory:
```powershell
.\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /PrepareAD /OrganizationName:"yourOrg"
#(if Exchange organization already exist in your environment, leave OrganizationName parameter)
#.\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /PrepareAD)
```
6) Prepare Domain:
```powershell
.\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF /PrepareAllDomains
```

