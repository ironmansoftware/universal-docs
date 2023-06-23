---
description: Grid layout component for Universal Apps.
---

# Grid

The responsive layout grid adapts to screen size and orientation, ensuring consistency across layouts.

The grid creates visual consistency between layouts while allowing flexibility across a wide variety of designs. Material Design’s responsive UI is based on a 12-column grid layout.

## Basic Layout

![](<../../../.gitbook/assets/image (341).png>)

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

## API

* [New-UDGrid](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDGrid.txt)

