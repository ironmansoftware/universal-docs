---
description: Examples of things you can do with dashboards.
---

# Examples

## Create User Form

This example shows how to create a local user account.&#x20;

```powershell
New-UDDashboard -Title 'New User' -Content {
    New-UDForm -Content {
        New-UDTextbox -Id 'UserName' -Label "User Name"
        New-UDTextbox -Id 'Password' -Label 'Password' -Type 'password'
    } -OnSubmit {
        $Password = $EventData.Password | ConvertTo-SecureString -AsPlainText
        New-LocalUser -Name $EventData.UserName -Password $Password
        Show-UDToast "New user $($EventData.UserName) was created!"
    }
}
```

## Stopwatch

This example shows how to create a stopwatch component in PowerShell Universal Dashboard.

```powershell
New-UDDashboard -Title 'Stopwatch' -Content {
    New-UDDynamic -Id 'stopwatch' -Content {
        (Get-Date).ToString('T')
    } -AutoRefresh -AutoRefreshInterval 1
    
    New-UDButton -Text 'Toggle Stopwatch' -OnClick {
        Set-UDElement -Id 'stopwatch' -Properties @{
            autoRefresh = -not( (Get-UDElement -Id 'stopwatch').AutoRefresh)
        }
    }
}
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
