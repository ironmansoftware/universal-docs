---
description: This sample creates a tree view of the OUs within Active Directory.
---

# Active Directory Tree View

```powershell
New-UDApp -Title "New-UDTree Active Directory Example" -Content {
    $RootDN = "OU=Users,DC=ironman,DC=local" 
    $OUList = Get-ADOrganizationalUnit -Filter * -SearchBase $RootDN -SearchScope Subtree -Properties ParentGuid -ErrorAction SilentlyContinue | Sort-Object Name | Select-Object Name, DistinguishedName, ParentGuid
    $AllOrganizationalUnits = @()
    foreach ($OU in $OUList) {
        if (!($OU.DistinguishedName -eq $RootDN)) {
            $ParentGuid = ([GUID]$OU.ParentGuid).Guid
            $ParentOU = Get-ADObject -Identity $ParentGuid -ErrorAction SilentlyContinue
            if ($ParentOU) {
                $AllOrganizationalUnits += [PSCustomObject]@{
                    Name              = $OU.Name
                    DistinguishedName = $OU.DistinguishedName
                    ParentDn          = $ParentOU.DistinguishedName
                }
            }
        }
    }
    New-UDTreeView -Node {
        foreach ($ou in $AllOrganizationalUnits) {
            if ( $ou.ParentDn -eq $RootDN ) {
                New-UDTreeNode -Name $ou.Name -id $ou.DistinguishedName 
            }
        }
    } -OnNodeClicked {
        $SubOUs = $AllOrganizationalUnits | Where-Object { $_.ParentDn -eq $eventdata.id } | Sort-Object Name
        foreach ($SubOU in $SubOUs) {
            New-UDTreeNode -Name $SubOU.Name -Id $SubOU.DistinguishedName
        }
        $SelectedOU = $(ConvertFrom-Json $body).Id
        Show-UDToast -Message $SelectedOU -Duration 6000
    }
}
```
