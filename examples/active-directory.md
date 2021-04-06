---
description: Active Directory examples for PowerShell Universal.
---

# Active Directory

## List Locked Accounts

This example uses [Universal Automation](../automation/about.md).

Shows an example of how to list locked Active Directory accounts. This example assumes that the user running PowerShell Universal has access to the local Active Directory environment. 

```PowerShell
Start-PSUServer -Port 8080 -Configuration {
    New-PSUScript -Name 'LockedAccounts' -ScriptBlock {
        Search-ADAccount -LockedOut
    }
}
```

Locked accounts will be listed on the job page's pipeline output. 

![](../.gitbook/assets/image%20%28198%29.png)

You can also access the locked accounts by using the Universal PowerShell module.

```PowerShell
$Job = Get-PSUJob -Script (Get-PSUScript -name 'LockedAccounts.ps1') -First 1 -OrderDirection Descending
Get-PSUJobPipelineOuptut -Job $Job
```



## Reset Password

This example uses [Universal Automation](../automation/about.md).

Shows an example of how to reset an Active Directory user account using PowerShell Universal Automation. This script accepts the identity of the account to reset, the password to set, whether to unlock the account and whether to require the user to change their password on logon.

```PowerShell
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

## Restore Deleted User

This account users PowerShell Universal [Dashboard ](../dashboard/about.md)and [Automation](../automation/about.md). 

In this example, we use Universal Dashboard to create a dashboard that displays a table that includes all the deleted user accounts for the domain. It creates a custom column with a button that includes a Restore button that executes a script to restore the specified account. This example assumes that the identity running the script is capable of accessing Active Directory. 

```PowerShell
Start-PSUServer -Port 8080 -Configuration {
    New-PSUScript -Name 'Restore User.ps1' -ScriptBlock {
        param($DistinguishedName)

        Restore-ADObject -Identity $DistinguishedName
    }

    New-PSUDashboard -Name 'Restore User' -BaseUrl '/' -Framework 'UniversalDashboard:Latest' -Content {
        New-UDDashboard -Title 'Restore User' -Content {
            $Columns = @(
                New-UDTableColumn -Property Name -Title "Name"
                New-UDTableColumn -Property DistinguishedName -Title "Distinguished Name"
                New-UDTableColumn -Property Restore -Title Restore -Render {
                    $Item = $EventData
                    New-UDButton -Id "btn$($Item.ObjectGuid)" -Text "Restore" -OnClick { 
                        Show-UDToast -Message "Restoring user $($Item.Name)" -Duration 5000
    
                        Invoke-UAScript -Name 'Restore User.ps1' -DistinguishedName $Item.DistinguishedName | Tee-Object -Variable job | Wait-UAJob
    
                        $Job = Get-UAJob -Id $Job.Id 
                        if ($Job.Status -eq 'Completed')
                        {
                            Show-UDToast -Message "Restored user $($Item.Name)" -Duration 5000
                        }
                        else 
                        {
                            $Output = Get-UAJobOutput -JobId $Job.Id | Select-Object -Expand Message
                            Show-UDToast -Message "Failed to restore user. $($Output -join "`n")" -BackgroundColor red -MessageColor white -Duration 5000
                        }
                    }
                }
            )
    
            $DeletedUsers = Get-ADObject -Filter 'IsDeleted -eq $true -and objectClass -eq "user"' -IncludeDeletedObjects | ForEach-Object {
                @{
                    distinguishedname = $_.DistinguishedName
                    name = $_.Name
                }
            }
            New-UDTable -Data $DeletedUsers -Columns $Columns
        }
    }
}
```

![](../.gitbook/assets/image%20%28202%29.png)

