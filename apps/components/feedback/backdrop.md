---
description: Backdrop component for Universal Apps.
---

# Backdrop

The backdrop component places an overlay over the drop of the entire page. It's useful for displaying loading states.

## Basic Backdrop

To create a basic backdrop, you can use the `New-UDBackdrop` cmdlet and include content to show within the backdrop. The content will be centered on the page. To show the backdrop, use the `-Open` switch parameter.

```powershell
New-UDBackdrop -Content {
    New-UDTypography -Text "Loading..." -Variant h2
} -Open
```

![Backdrop component](<../../../.gitbook/assets/image (53).png>)

## OnClick Handler

The backdrop provides an `-OnClick` handler that you can use to close the backdrop when clicked. You can use `Set-UDElement` to open and close the backdrop.

```powershell
New-UDBackdrop -Id 'backdrop' -Content {
    New-UDTypography -Text "Loading..." -Variant h2
} -Open -OnClick {
    Set-UDElement -Id 'backdrop' -Properties @{
        open = $false
    }
}
```

## API&#x20;

* [New-UDBackdrop](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDBackdrop.txt)
