---
description: UDStyle component for Universal Dashboard
---

# Styles

You can apply styles to individual components within Universal Dashboard by using the `UDStyle` component. This component can be found on the [Universal Dashboard Marketplace](https://marketplace.universaldashboard.io/Dashboard/UniversalDashboard.Style).

## Applying a Style

To apply a style to a component or a set of components, you call the `New-UDStyle` cmdlet, specify a CSS style and then include the components you wish to style within the `-Content` script block.

```PowerShell
New-UDStyle -Style '
    padding: 32px;
    background-color: hotpink;
    font-size: 24px;
    border-radius: 4px;
    &:hover {
      color: white;
    }
    .card {
        background-color: green !important;   
    }' -Content {
        New-UDCard -Title 'Test' -Content {
            "Hello"
        }
    }
```

![UDStyled card](../../.gitbook/assets/image%20%28168%29.png)

