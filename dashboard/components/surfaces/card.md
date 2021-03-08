---
description: Card component for Universal Dashboard
---

# Card

**Cards contain content and actions about a single subject.**

Cards are surfaces that display content and actions on a single topic. They should be easy to scan for relevant and actionable information. Elements, like text and images, should be placed on them in a way that clearly indicates hierarchy.

## Simple Card

Although cards can support multiple actions, UI controls, and an overflow menu, use restraint and remember that cards are entry points to more complex and detailed information.

![](../../../.gitbook/assets/image%20%2856%29.png)

```text
New-UDCard -Title 'Simple Card' -Content {
    "This is some content"
}
```

## Advanced Card

You can use the body, header, footer and expand cmdlets to create advanced cards. The below example creates a card with various features based on a Hyper-V VM. 

```text
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

![Expandable Card](../../../.gitbook/assets/image%20%28220%29.png)

**New-UDCard**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| ClassName | String | A CSS class to assign to this card. | false |
| ShowToolBar | SwitchParameter | Whether to show the toolbar for this card. | false |
| ToolBar | Object | The toolbar for this card. Use New-UDCardToolbar to create a toolbar. | false |
| Header | Object | The header for this card. The header typically contains a title for the card. Use New-UDCardHeader to create a header. | false |
| Body | Object | The body for this card. This is the main content for the card. Use New-UDCardHeader to create a body. | false |
| Expand | Object | Th expand content for this card. Expand content is show when the user clicks the expansion button. Use New-UDCardExpand to create an expand. | false |
| Footer | Object | The footer for this card. Footer contents typically contain actions that are relavent to the card. Use New-UDCardFooter to create a footer. | false |
| Style | Hashtable | Styles to apply to the card. | false |
| Elevation | Int32 | The amount of elevation to provide the card. The more elevation, the more it will appear the card is floating off the page. | false |
| Title | String | A title for the card. | false |
| TitleAlignment | String | The alignment for the title. | false |
| Content | ScriptBlock | The content of the card. | false |
| Image | String | An image to show in the card. | false |

