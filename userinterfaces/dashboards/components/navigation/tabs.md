---
description: Tab component for Universal Dashboard
---

# Tabs

**Tabs make it easy to explore and switch between different views.**

Tabs organize and allow navigation between groups of content that are related and at the same level of hierarchy.

## Tabs

![](../../../../.gitbook/assets/image%20%2840%29.png)

```text
New-UDTabs -Tabs {
    New-UDTab -Text 'Item One' -Content { New-UDTypography -Text 'Item One' -Variant 'h2' }
    New-UDTab -Text 'Item Two' -Content { New-UDTypography -Text 'Item Two' -Variant 'h2' }
    New-UDTab -Text 'Item Three' -Content { New-UDTypography -Text 'Item Three' -Variant 'h2' }
}
```

## Vertical Tabs

![](../../../../.gitbook/assets/image%20%2874%29.png)

```text
New-UDTabs -Tabs {
    New-UDTab -Text 'Item One' -Content { New-UDTypography -Text 'Item One' -Variant 'h2' }
    New-UDTab -Text 'Item Two' -Content { New-UDTypography -Text 'Item Two' -Variant 'h2' }
    New-UDTab -Text 'Item Three' -Content { New-UDTypography -Text 'Item Three' -Variant 'h2' }
} -Orientation vertical
```

## Dynamic Tabs

Dynamic tabs will refresh their content when they are selected. You will need to include the `-RenderOnActive` parameter to prevent all the tabs from rendering even if they are not shown.

```text
New-UDTabs -Tabs {
    New-UDTab -Text 'Item One' -Content { Get-Date } -Dynamic
    New-UDTab -Text 'Item Two' -Content { Get-Date } -Dynamic
    New-UDTab -Text 'Item Three' -Content { Get-Date } -Dynamic
} -RenderOnActive
```

**New-UDTabs**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Tabs | ScriptBlock | The tabs to put within this container. | true |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| RenderOnActive | SwitchParameter | Whether to render the tabs when they are clicked. Is this value isn't present, all the tabs are rendered, even if they are not shown. | false |
| Orientation | String | The orientation of the tabs. | false |

**New-UDTab**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Text | string | The text to display in the header. | false |
| Content | scriptblock | The content of the tab. | true |
| Id | string | The ID of the tab. | false |
| Dynamic | switch | A dynamic tab will reload every time it is selected. | false |
| Icon | Object |  | false |
| Stacked | switch |  | false |

