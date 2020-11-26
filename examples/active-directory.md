---
description: Active Directory examples for PowerShell Universal.
---

# Active Directory

## Reset Password

Shows an example of how to reset an Active Directory user account using PowerShell Universal Automation. This script accepts the identity of the account to reset, the password to set, whether to unlock the account and whether to require the user to change their password on logon.

```text
Start-PSUServer -Port 8080 -Configuration {
    New-PSUScript -Name 'Reset Password' -ScriptBlock {
        param(
            [String]$Identity,
            [String]$Password,
            [Switch]$Unlock,
            [Switch]$ChangePasswordOnLogon
        )
        
        $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
        
        Set-ADAccountPassword -Identity $Identity -NewPassword $SecurePassword -Reset -Server $ComputerName -Credential $Domain
        
        if ($Unlock)
        {
            Unlock-ADAccount –Identity $Identity -Server $ComputerName -Credential $Domain
        }
        
        if ($ChangePasswordOnLogon)
        {
            Set-ADUser –Identity $Identity -ChangePasswordAtLogon $true -Server $ComputerName -Credential $Domain
        }
    }
}
```

![](../.gitbook/assets/image%20%28197%29.png)



