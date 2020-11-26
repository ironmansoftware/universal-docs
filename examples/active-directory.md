---
description: Active Directory examples for PowerShell Universal.
---

# Active Directory

## Reset Password

Reset Active Directory User passwords. 

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



