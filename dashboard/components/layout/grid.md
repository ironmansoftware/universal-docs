---
description: Grid layout component for Universal Dashboard.
---

# Grid

The responsive layout grid adapts to screen size and orientation, ensuring consistency across layouts.

The grid creates visual consistency between layouts while allowing flexibility across a wide variety of designs. Material Design’s responsive UI is based on a 12-column grid layout.

## Basic Layout

![](../../../.gitbook/assets/image%20%2857%29.png)

```PowerShell
New-UDGrid -Container -Content {
    New-UDGrid -Item -ExtraSmallSize 12 -Content {
        New-UDPaper -Content { "xs-12" } -Elevation 2
    }
    New-UDGrid -Item -ExtraSmallSize 6 -Content {
        New-UDPaper -Content { "xs-6" } -Elevation 2
    }
    New-UDGrid -Item -ExtraSmallSize 6 -Content {
        New-UDPaper -Content { "xs-6" } -Elevation 2
    }
    New-UDGrid -Item -ExtraSmallSize 3 -Content {
        New-UDPaper -Content { "xs-3" } -Elevation 2
    }
    New-UDGrid -Item -ExtraSmallSize 3 -Content {
        New-UDPaper -Content { "xs-3" } -Elevation 2
    }
    New-UDGrid -Item -ExtraSmallSize 3 -Content {
        New-UDPaper -Content { "xs-3" } -Elevation 2
    }
    New-UDGrid -Item -ExtraSmallSize 3 -Content {
        New-UDPaper -Content { "xs-3" } -Elevation 2
    }
}
```

## Spacing

Adjust the spacing between items in the grid

```PowerShell
New-UDDynamic -Id 'spacingGrid' -Content {
    $Spacing = (Get-UDElement -Id 'spacingSelect').value

    New-UDGrid -Spacing $Spacing -Container -Content {
        New-UDGrid -Item -ExtraSmallSize 3 -Content {
            New-UDPaper -Content { "xs-3" } -Elevation 2
        }
        New-UDGrid -Item -ExtraSmallSize 3 -Content {
            New-UDPaper -Content { "xs-3" } -Elevation 2
        }
        New-UDGrid -Item -ExtraSmallSize 3 -Content {
            New-UDPaper -Content { "xs-3" } -Elevation 2
        }
        New-UDGrid -Item -ExtraSmallSize 3 -Content {
            New-UDPaper -Content { "xs-3" } -Elevation 2
        }
    }
}

New-UDSelect -Id 'spacingSelect' -Label Spacing -Option {
    for($i = 0; $i -lt 10; $i++)
    {
        New-UDSelectOption -Name $i -Value $i
    }
} -OnChange { Sync-UDElement -Id 'spacingGrid' } -DefaultValue 3
```

## Row and Columns

You can also use the `New-UDRow` and `New-UDColumn` functions when working with the grid. 

```PowerShell
New-UDRow -Columns {
    New-UDColumn -SmallSize 12 -Content {
        New-UDPaper -Content { "xs-12" } -Elevation 2
    }
    New-UDColumn -SmallSize 12 -Content {
        New-UDPaper -Content { "xs-12" } -Elevation 2
    }
}
```

**New-UDGrid**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| ExtraSmallSize | Int32 | The size \(1-24\) for extra small devices. | false |
| SmallSize | Int32 | The size \(1-24\) for small devices. | false |
| MediumSize | Int32 | The size \(1-24\) for medium devices. | false |
| LargeSize | Int32 | The size \(1-24\) for large devices. | false |
| ExtraLargeSize | Int32 | The size \(1-24\) for extra large devices. | false |
| Container | SwitchParameter | Whether this is a container. A container can be best described as a row. | false |
| Spacing | Int32 | Spacing between the items. | false |
| Item | SwitchParameter | Whether this is an item in a container. | false |
| Children | ScriptBlock | Components included in this grid item. | false |

