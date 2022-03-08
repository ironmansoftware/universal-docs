---
description: UDStyle component for Universal Dashboard
---

# Styles

You can apply styles to individual components within Universal Dashboard by using the `UDStyle` component. This component will need to be added to your dashboard and is part of the core components included with PowerShell Universal.

## Applying a Style

To apply a style to a component or a set of components, you call the `New-UDStyle` cmdlet, specify a CSS style and then include the components you wish to style within the `-Content` script block.

```powershell
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

![UDStyled card](<../../../.gitbook/assets/image (158).png>)

## Overriding Built in Styles

Each Material UI component has a set of built in classes that you can override using `New-UDStyle`. To determine the class names that you need to override, you can view the API documentation for the component you are trying to modify on the Material UI site. For example, here is a listing of the Alert component's CSS [class names](https://material-ui.com/api/alert/#css).

When using a success alert, you will have the `.MuiAlert-standardSuccess` class applied to your component. You can override this default style like this.

```powershell
New-UDStyle -Style '.MuiAlert-standardSuccess { background-color: red !important;  }  ' -Content {
    New-UDAlert -Text "Hello"
}
```

The resulting alert will be red instead of the default green.

![Alert with Red Background](<../../../.gitbook/assets/image (213).png>)
