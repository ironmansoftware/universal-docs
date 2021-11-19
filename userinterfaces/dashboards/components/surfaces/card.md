---
description: Card component for Universal Dashboard
---

# Card

**Cards contain content and actions about a single subject.**

Cards are surfaces that display content and actions on a single topic. They should be easy to scan for relevant and actionable information. Elements, like text and images, should be placed on them in a way that clearly indicates hierarchy.

## Simple Card

Although cards can support multiple actions, UI controls, and an overflow menu, use restraint and remember that cards are entry points to more complex and detailed information.

![](<../../../../.gitbook/assets/image (56).png>)

```powershell
New-UDCard -Title 'Simple Card' -Content {
    "This is some content"
}
```

## Advanced Card

You can use the body, header, footer and expand cmdlets to create advanced cards. The below example creates a card with various features based on a Hyper-V VM.

```powershell
$VM = Get-VM -Name $VMName @ConnectionInfo

$Header = New-UDCardHeader -Title $VM.Name

$Footer = New-UDCardFooter -Content {
    if ($VM.State -eq 'Running')
    {
        New-UDButton -Variant text -Text 'Stop' -OnClick {
            Show-UDToast -Message 'Stopping VM...' -Duration 5000
            Stop-VM -VMName $VM.name @ConnectionInfo 
            Sync-UDElement -Id "$($VMName)_card"
        }
    } else {
        New-UDButton -Variant text -Text 'Start' -OnClick {
            Show-UDToast -Message 'Starting VM...' -Duration 5000
            Start-VM -VMName $VM.name @ConnectionInfo 
            Sync-UDElement -Id "$($VMName)_card"
        }
    }

}

$Body = New-UDCardBody -Content {
    New-UDTable -Data ($VM | Select-Object Name, State, CPUUsage, MemoryAssigned, Uptime)  -Dense 
}

$Expand = New-UDCardExpand -Content {
    New-UDElement -Tag 'div' -Content {
        New-UDTable -Data ($VM.DvdDrives | Select-Object Name, DvdMediaType, Path) -Title 'DVD Drives' -Dense
    } 

    $Drives = Get-VMHardDiskDrive -VMName $VM.Name @ConnectionInfo | Select-Object Name, Path
    New-UDTable -Data $Drives -Title 'Hard Disk Drives' -Dense

    New-UDTable -Data ($VM.NetworkAdapters | Select-Object 'SwitchName', 'MacAddress' ) -Dense -Title 'Network Adapters' 
}

New-UDStyle -Style '.ud-mu-cardexpand { display: block !important }' -Content {
    New-UDCard -Body $Body -Header $Header -Footer $Footer -Expand $Expand
}
```

![Expandable Card](<../../../../.gitbook/assets/image (220).png>)

## API

* [New-UDCard](../../../../cmdlets/New-UDCard.txt)
* [New-UDCardBody](../../../../cmdlets/New-UDCardBody.txt)
* [New-UDCardExpand](../../../../cmdlets/New-UDCardExpand.txt)
* [New-UDCardFooter](../../../../cmdlets/New-UDCardFooter.txt)
* [New-UDCardHeader](../../../../cmdlets/New-UDCardHeader.txt)
* [New-UDCardMedia](../../../../cmdlets/New-UDCardMedia.txt)
* [New-UDCardToolbar](../../../../cmdlets/New-UDCardToolbar.txt)
