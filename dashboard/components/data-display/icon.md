---
description: Icon component for Universal Dashboard
---

# Icon

FontAwesome icons to include in your dashboard.

![](../../../.gitbook/assets/image%20%2869%29.png)

## Visually Search for Icons

```text
New-UDTextbox -Id 'txtIconSearch' -Label 'Search' 
New-UDButton -Text 'Search' -OnClick {
    Sync-UDElement -Id 'icons'
}

New-UDElement -tag 'p' -Content {}

New-UDDynamic -Id 'icons' -Content {
        $Icons = [Enum]::GetNames([UniversalDashboard.Models.FontAwesomeIcons])
        $IconSearch = (Get-UDElement -Id 'txtIconSearch').value
        if ($null -ne $IconSearch -and $IconSearch -ne '')
        {
        $Icons = $Icons.where({ $_ -match $IconSearch})
    }

    foreach($icon in $icons) {
        New-UDIcon -Icon $icon -Size lg
    }
}
```



**New-UDIcon**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string |  | false |
| Icon | FontAwesomeIcons |  | false |
| FixedWidth | switch |  | false |
| Inverse | switch |  | false |
| Rotation | int |  | false |
| ClassName | string |  | false |
| Transform | string |  | false |
| Flip | string |  | false |
| Pull | string |  | false |
| ListItem | switch |  | false |
| Spin | switch |  | false |
| Border | switch |  | false |
| Pulse | switch |  | false |
| Size | string |  | false |
| Style | hashtable |  | false |
| Title | string |  | false |
| Regular | switch |  | false |
| Color |  |  |  |

