---
description: Grid layout component for Universal Dashboard.
---

# Grid

The responsive layout grid adapts to screen size and orientation, ensuring consistency across layouts.

The grid creates visual consistency between layouts while allowing flexibility across a wide variety of designs. Material Design’s responsive UI is based on a 12-column grid layout.

## Basic Layout

![](<../../../../.gitbook/assets/image (57).png>)

```powershell
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

```powershell
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

```powershell
New-UDRow -Columns {
    New-UDColumn -SmallSize 12 -Content {
        New-UDPaper -Content { "xs-12" } -Elevation 2
    }
    New-UDColumn -SmallSize 12 -Content {
        New-UDPaper -Content { "xs-12" } -Elevation 2
    }
}
```

## Adaptive Sizing

`New-UDColumn` provides multiple sizing parameters for different screen sizes. This allows you to use the same components but different layouts when viewed from different screen sizes. The following parameters control the size of the column based on screen size:

* \-ExtraLargeSize
* \-LargeSize
* \-MediumSize
* \-SmallSize

The following example creates a different layout for the different screen sizes.&#x20;

```powershell
New-UDRow -Columns {
    New-UDColumn -SmallSize 12 -MediumSize 6 -LargeSize 4 -Content {
        New-UDPaper -Content { "xs-12" } -Elevation 2
    }
    New-UDColumn -SmallSize 12 -MediumSize 6 -LargeSize 4 -Content {
        New-UDPaper -Content { "xs-12" } -Elevation 2
    }
    New-UDColumn -SmallSize 12 -MediumSize 6 -LargeSize 4 -Content {
        New-UDPaper -Content { "xs-12" } -Elevation 2
    }
}
```

If a screen size is not specified, the next one down would be used. For example, if only `-SmallSize` was specified, it would be used for all screen sizes.

## API

* [New-UDGrid](../../../../cmdlets/New-UDGrid.txt)

****
