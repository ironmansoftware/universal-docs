---
description: Examples of things you can do with apps.
---

# Examples

## Display Processes

This example displays processes in a table.&#x20;

```powershell
New-UDApp -Title 'Processes' -Content {
    $Processes = Get-Process | Select-Object Id, Name
    New-UDTable -Columns @(
        New-UDTableColumn -Property 'Id' -Title 'Id'
        New-UDTableColumn -Property 'Name' -Title 'Name'
    ) -Data $Processes -ShowPagination
}
```

<figure><img src="../.gitbook/assets/image (355).png" alt=""><figcaption></figcaption></figure>

## File System Browser

Create a file system browser with a dynamic tree view.&#x20;

```powershell
New-UDApp -Title 'Processes' -Content {
    Get-PSDrive -PSProvider 'FileSystem' | ForEach-Object {
        New-UDTreeView -Node { New-UDTreeNode -Name $_.Name -Id "$($_.Name):\" } -OnNodeClicked {
            Get-ChildItem $EventData.Id | ForEach-Object {
                New-UDTreeNode -Name $_.Name -Id $_.FullName -Leaf:$(-not $_.PSIsContainer)
            }
        }
    }
}
```

<figure><img src="../.gitbook/assets/image (305).png" alt=""><figcaption></figcaption></figure>

## Create User Form

This example shows how to create a local user account.&#x20;

```powershell
New-UDApp -Title 'New User' -Content {
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

<figure><img src="../.gitbook/assets/image (530).png" alt=""><figcaption></figcaption></figure>

## Clock

This example shows how to create a clock component in PowerShell Universal.

```powershell
New-UDApp -Title 'Clock' -Content {
    New-UDDynamic -Id 'clock' -Content {
        (Get-Date).ToString('T')
    } -AutoRefresh -AutoRefreshInterval 1
    
    New-UDButton -Text 'Toggle Clock' -OnClick {
        Set-UDElement -Id 'clock' -Properties @{
            autoRefresh = -not( (Get-UDElement -Id 'clock').AutoRefresh)
        }
    }
}
```

<figure><img src="../.gitbook/assets/image (187).png" alt=""><figcaption></figcaption></figure>
