---
description: Build custom components.
---

# Custom Components

Components in PowerShell Universal apps are exposed as functions. You can combine built in components to produce your own custom components.

## Example: People Picker

<figure><img src="../../../.gitbook/assets/image (506).png" alt=""><figcaption><p>People Picker</p></figcaption></figure>

The below example creates a `New-UDPeoplePicker` component from existing app components. You can use the `New-UDPeoplePicker` component in your apps. This function can either be defined within your app directly or within a [Module](../../../platform/modules.md).

This example users a published folder of avatars.

```powershell
function Get-User {
    1..100 | ForEach-Object {
        [PSCustomObject]@{
            UserName = "User$_"
            First = "Bill"
            Last = $_
            Avatar = (Get-ChildItem "$Repository\Avatars" | Get-Random).Name
        }
    }
}

function New-UDPeoplePicker {
   $Session:Users = [System.Collections.Generic.List[object]]::new()

    New-UDAutocomplete -OnLoadOptions {
        Get-User | Where-Object { $_.UserName -like "*$UserName*" } | Select-Object -First 5 -ExpandProperty 'UserName' | ConvertTo-Json 
    } -OnChange {
        $Session:Users.Add((Get-User | Where-Object { $_.UserName -eq $EventData })) | Out-Null
        Sync-UDElement -Id 'users'
    }

    New-UDDynamic -Id 'users' -Content {
        New-UDList -Children {
            $Session:Users | ForEach-Object {
                New-UDListItem -Label $_.UserName -SubTitle "$($_.First) $($_.Last)" -AvatarType 'Avatar' -SecondaryAction {
                    $UserName = $_.UserName
                    New-UDIconButton -Icon (New-UDIcon -Icon 'Trash') -OnClick {
                        $RemoveUser = $Session:Users | Where-Object { $_.UserName -eq $UserName }
                        $Session:Users.Remove($RemoveUser) 
                        Sync-UDElement -Id 'users'
                    }
                } -Source "/avatars/$($_.Avatar)"

            }    
        }
    }
}

New-UDApp -Title 'PowerShell Universal' -Content {
    New-UDPeoplePicker
}
```
