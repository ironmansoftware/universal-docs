---
description: AppBar component for Universal Apps
---

# AppBar

**The App Bar displays information and actions relating to the current screen.**

The top App Bar provides content and actions related to the current screen. It's used for branding, screen titles, navigation, and actions.

## AppBar with Custom Drawer

![](<../../../.gitbook/assets/image (501).png>)

```powershell
$Drawer = New-UDDrawer -Children {
    New-UDList -Children {
        New-UDListItem -Label "Home"
        New-UDListItem -Label "Getting Started" -Children {
            New-UDListItem -Label "Installation" -OnClick {}
            New-UDListItem -Label "Usage" -OnClick {}
            New-UDListItem -Label "FAQs" -OnClick {}
            New-UDListItem -Label "System Requirements" -OnClick {}
            New-UDListItem -Label "Purchasing" -OnClick {}
        }
    }
}

New-UDAppBar -Position relative -Children { New-UDElement -Tag 'div' -Content { "Title" } } -Drawer $Drawer
```

## Footer

To create an app bar that is pinned to the bottom of the page, you can use the `-Footer` parameter.

```powershell
New-UDAppBar -Children { "Hello" } -Footer
```

## Fixed AppBar

A fixed AppBar will show even when the screen is scrolled. It will remain stuck to the top. This example creates an AppBar that is fixed with a div that is 10000 pixels high.

```powershell
New-UDAppBar -Position fixed -Children { New-UDElement -Tag 'div' -Content { "Title" } }

New-UDElement -Tag 'div' -Content {

} -Attributes @{
    style = @{
        height = "10000px"
    }
}
```

## API&#x20;

* [New-UDAppBar](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDAppBar.txt)
