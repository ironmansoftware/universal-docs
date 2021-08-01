---
description: Icon component for Universal Dashboard
---

# Icon

[FontAwesome ](https://fontawesome.com/?from=io)icons to include in your dashboard.

![](../../../../.gitbook/assets/image%20%2872%29.png)

## Icon

Create icons by specifying their names. You can use the icon reference below to find icons.

```text
New-UDIcon -Icon 'address_book'
```

![](../../../../.gitbook/assets/image%20%28109%29.png)

## Size

Set the size of the icon. Valid values are: `xs`, `sm`, `lg`, `2x`, `3x`, `4x`, `5x`, `6x`, `7x`, `8x`, `9x`, `10x`

```text
    New-UDIcon -Icon 'address_book' -Size 'sm'
    New-UDIcon -Icon 'address_book' -Size 'lg'
    New-UDIcon -Icon 'address_book' -Size '5x'
    New-UDIcon -Icon 'address_book' -Size '10x'
```

![](../../../../.gitbook/assets/image%20%28111%29.png)

## Rotation

Rotate icons. The value represents the degrees of rotation.

```text
New-UDIcon -Icon 'address_book' -Size '5x' -Rotation 90
```

![](../../../../.gitbook/assets/image%20%28110%29.png)

## Border

Add a border to your icon.

```text
New-UDIcon -Icon 'address_book' -Size '5x' -Border
```

![](../../../../.gitbook/assets/image%20%28108%29.png)

## Style

Apply CSS styles to your icon.

```text
New-UDIcon -Icon 'address_book' -Size '5x' -Style @{
    backgroundColor = "red"
}
```

![](../../../../.gitbook/assets/image%20%28112%29.png)

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

## Parameters

**New-UDIcon**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string | Id of the icon | false |
| Icon | FontAwesomeIcons | Icon to select | false |
| FixedWidth | switch |  | false |
| Inverse | switch | Whether to inverse the icon | false |
| Rotation | int | Rotates an icon clockwise based on the degrees specified | false |
| ClassName | string |  | false |
| Transform | string |  | false |
| Flip | string |  | false |
| Pull | string |  | false |
| ListItem | switch |  | false |
| Spin | switch | Caues the icon to spin. | false |
| Border | switch | Adds a border to the icon. | false |
| Pulse | switch |  | false |
| Size | string | The size of the icon | false |
| Style | hashtable | A CSS style to apply to the icon. | false |
| Title | string |  | false |
| Regular | switch |  | false |
| Color |  |  |  |



