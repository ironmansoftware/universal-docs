---
description: CVEs for PowerShell Universal.
---

# CVEs

Please report vulnerabilities to Ironman Software. To learn about our vulnerability response policy, [click here](https://ironmansoftware.com/vulnerability-response-policy/).

## CVE-2025-54552 - 7/25/2025 - Information disclosure

### Description

The PowerShell Universal Live App documentation lists all variables to authenticated users. The connection string variable is included in this list. Depending on database configuration, this can include plaintext credentials.&#x20;

Affected Versions: v4.5.4 and earlier, v5.6.0 and earlier

CVSS v4.0 Score: 8.7 / High: [AV:N/AC:L/PR:L/UI:R/S:C/C:H/I:H/A:H/E:H/RL:O/RC:C/CR:X/IR:X/AR:X/MAV:N/MAC:L/MPR:L/MUI:R/MS:C/MC:H/MI:H/MA:H](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator?vector=AV:N/AC:L/PR:L/UI:R/S:C/C:H/I:H/A:H/E:H/RL:O/RC:C/CR:X/IR:X/AR:X/MAV:N/MAC:L/MPR:L/MUI:R/MS:C/MC:H/MI:H/MA:H\&version=3.1)

### Workaround

In addition to upgrading to a patched version, you can also edit the installation media to remove the variable.&#x20;

Edit the file Docs\variables.ps1.

```powershell
New-UDPage -Name 'Variables' -Icon (New-UDIcon -Icon 'SquareRootVariable') -Content {
    $Variables = Get-Variable | Where-Object Name -ne PSUConnectionString | ForEach-Object {
        [PSCustomObject]@{
            Name        = $_.Name
            Value       = if ($_.Value -eq $null) { "$null" } else { $_.Value.ToString() }
            Description = $_.Description
        }
    }
    New-UDTable -Title 'Variables' -Data $Variables -Columns @(
        New-UDTableColumn -Property Name -Title 'Name'
        New-UDTableColumn -Property Value -Title 'Value'
        New-UDTableColumn -Property Description -Title 'Description'
    ) -ShowPagination -Dense -PageSize 10
}
```

## CVE-TBD - 2/18/2025 - Incorrect Access Controls

### Description

Due to an authorization issue with the PowerShell Universal v5.3.x's gRPC service registration, a remote attacker can access the server using the Universal PowerShell module without authentication.&#x20;

### CVSS v4.0 Score: 9.8 High

## CVE-2025-26792 - 1/29/2025 - Information disclosure

### Description

Version 4.5.x and 5.x.x are vulnerable to an information disclosure through directory traversal when using PowerShell Universal published folders. Systems that do not have this feature configured, are not affected. If authenticated published folders are configured, the attacker will need to be authenticated.&#x20;

### CVSS v4.0 Score: 5.4 / Medium

This exploit allows an attacker to expose information of the affected system, depending on system configuration.

## CVE-2024-50616 - 10/17/2024 - Privilege escalation and information disclosure

### Description

Version 5.0.0 through 5.0.11 are vulnerable to an exploit that allows an authenticated attacker to elevate their privileges and view job information.

### CVSS v4.0 Score: 7.4 / High

This exploit allows an authenticated attacker to take control of the platform via a vulnerability in the admin console.

###

###
