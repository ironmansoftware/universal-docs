---
description: Tab component for Universal Apps
---

# Tabs

**Tabs make it easy to explore and switch between different views.**

Tabs organize and allow navigation between groups of content that are related and at the same level of hierarchy.

## Tabs

![](<../../../.gitbook/assets/image (471).png>)

```powershell
New-UDTabs -Tabs {
    New-UDTab -Text 'Item One' -Content { New-UDTypography -Text 'Item One' -Variant 'h2' }
    New-UDTab -Text 'Item Two' -Content { New-UDTypography -Text 'Item Two' -Variant 'h2' }
    New-UDTab -Text 'Item Three' -Content { New-UDTypography -Text 'Item Three' -Variant 'h2' }
}
```

## Vertical Tabs

![](<../../../.gitbook/assets/image (106).png>)

```powershell
New-UDTabs -Tabs {
    New-UDTab -Text 'Item One' -Content { New-UDTypography -Text 'Item One' -Variant 'h2' }
    New-UDTab -Text 'Item Two' -Content { New-UDTypography -Text 'Item Two' -Variant 'h2' }
    New-UDTab -Text 'Item Three' -Content { New-UDTypography -Text 'Item Three' -Variant 'h2' }
} -Orientation vertical
```

## Dynamic Tabs

Dynamic tabs will refresh their content when they are selected. You will need to include the `-RenderOnActive` parameter to prevent all the tabs from rendering even if they are not shown.

```powershell
New-UDTabs -Tabs {
    New-UDTab -Text 'Item One' -Content { Get-Date } -Dynamic
    New-UDTab -Text 'Item Two' -Content { Get-Date } -Dynamic
    New-UDTab -Text 'Item Three' -Content { Get-Date } -Dynamic
} -RenderOnActive
```

## Icons

```powershell
New-UDTabs -Tabs {
    New-UDTab -Text 'Item One' -Content { New-UDTypography -Text 'Item One' -Variant 'h2' } -Icon (New-UDIcon -Icon Users)
    New-UDTab -Text 'Item Two' -Content { New-UDTypography -Text 'Item Two' -Variant 'h2' } -Icon (New-UDIcon -Icon Desktop)
    New-UDTab -Text 'Item Three' -Content { New-UDTypography -Text 'Item Three' -Variant 'h2' } -Icon (New-UDIcon -Icon Exclamation)
}
```

## API

* [New-UDTabs](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDStepper.txt)
* [New-UDTab](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDTab.txt)

