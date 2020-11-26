---
description: Active Directory examples for PowerShell Universal.
---

# Active Directory

## List Locked Accounts

This example uses [Universal Automation](../automation/about.md).

Shows an example of how to list locked Active Directory accounts. This example assumes that the user running PowerShell Universal has access to the local Active Directory environment. 

```text
Start-PSUServer -Port 8080 -Configuration {
    New-PSUScript -Name 'LockedAccounts' -ScriptBlock {
        Search-ADAccount -LockedOut
    }
}
```

Locked accounts will be listed on the job page's pipeline output. 

![](../.gitbook/assets/image%20%28198%29.png)

You can also access the locked accounts by using the Universal PowerShell module.

```text
$Job = Get-PSUJob -Script (Get-PSUScript -name 'LockedAccounts.ps1') -First 1 -OrderDirection Descending
Get-PSUJobPipelineOuptut -Job $Job
```



## Reset Password

This example uses [Universal Automation](../automation/about.md).

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



