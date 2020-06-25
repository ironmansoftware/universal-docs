---
description: Modal component for Universal Dashboard.
---

# Modal

Modals inform users about a task and can contain critical information, require decisions, or involve multiple tasks.

## Basic

![](../../../.gitbook/assets/image%20%2846%29.png)

```text
New-UDButton -Text 'Basic' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    }
}
```

## Full Screen

![](../../../.gitbook/assets/image%20%2879%29.png)

```text
New-UDButton -Text 'Full Screen' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    } -Footer {
        New-UDButton -Text "Close" -OnClick { Hide-UDModal }
    }  -FullScreen
}
```

## Full Width

![](../../../.gitbook/assets/image%20%2863%29.png)

```text
New-UDButton -Text 'Full Width' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    } -FullWidth -MaxWidth 'md'
}
```

## Persistent

![](../../../.gitbook/assets/image%20%2845%29.png)

```text
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
| FullScreen | switch |  | false |
| Footer | scriptblock |  | false |
| Header | scriptblock |  | false |
| Content | scriptblock |  | false |
| Persistent | switch |  | false |
| FullWidth | switch |  | false |
| MaxWidth | string |  | false |

