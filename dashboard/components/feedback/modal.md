---
description: Modal component for Universal Dashboard.
---

# Modal

Modals inform users about a task and can contain critical information, require decisions, or involve multiple tasks.

## Basic

![](../../../.gitbook/assets/image%20%2846%29.png)

```PowerShell
New-UDButton -Text 'Basic' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    }
}
```

## Full Screen

![](../../../.gitbook/assets/image%20%2879%29.png)

```PowerShell
New-UDButton -Text 'Full Screen' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    } -Footer {
        New-UDButton -Text "Close" -OnClick { Hide-UDModal }
    }  -FullScreen
}
```

## Full Width

Full width modals take up the full width as defined by the `-MaxWidth` parameter. 

![](../../../.gitbook/assets/image%20%2863%29.png)

```PowerShell
New-UDButton -Text 'Full Width' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    } -FullWidth -MaxWidth 'md'
}
```

## Persistent

Persistent modals do not close when you click off of them. You will have to close it with `Hide-UDModal`.

![](../../../.gitbook/assets/image%20%2845%29.png)

```PowerShell
New-UDButton -Text 'Persistent' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    } -Footer {
        New-UDButton -Text "Close" -OnClick { Hide-UDModal }
    } -Persistent
}
```



**Show-UDModal**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| FullScreen | switch | Creates a full screen modal | false |
| Footer | ScriptBlock | Sets the footer content for the modal. | false |
| Header | ScriptBlock | Sets the header content for the modal. | false |
| Content | ScriptBlock | Sets the main body content for the modal. | false |
| Persistent | switch | Creates a persistent modal. | false |
| FullWidth | switch | Creates a full width modal. | false |
| MaxWidth | string | Defines the max width of a full width modal. | false |

