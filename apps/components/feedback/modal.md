---
description: Modal component for Universal Apps.
---

# Modal

Modals inform users about a task and can contain critical information, require decisions, or involve multiple tasks.

## Basic

![](<../../../.gitbook/assets/image (416).png>)

```powershell
New-UDButton -Text 'Basic' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    }
}
```

## Full Screen

![](<../../../.gitbook/assets/image (330).png>)

```powershell
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

![](<../../../.gitbook/assets/image (535).png>)

```powershell
New-UDButton -Text 'Full Width' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    } -FullWidth -MaxWidth 'md'
}
```

## Persistent

Persistent modals do not close when you click off of them. You will have to close it with `Hide-UDModal`.

![](<../../../.gitbook/assets/image (527).png>)

```powershell
New-UDButton -Text 'Persistent' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    } -Footer {
        New-UDButton -Text "Close" -OnClick { Hide-UDModal }
    } -Persistent
}
```

## Hide a Modal

You can use the `Hide-UDModal` button to hide a modal that is currently show.

```powershell
New-UDButton -Text 'Basic' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    }
    Start-Sleep 5
    Hide-UDModal
}
```

## Styling

You can style modules using the `-Style`, `-HeaderStyle`, `-ContentStyle` and `-FooterStyle` parameters. Style is applied to the entire modal itself and the individual section styles are only applied to those sections. The value for these parameters are hashtables of CSS values.&#x20;

```powershell
New-UDButton -Text 'Styling' -OnClick {
    Show-UDModal -Content {
        New-UDTypography -Text "Hello"
    } -Style @{
        backgroundColor = "red"
    }
}
```

## API

* [Show-UDModal](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Show-UDModal.txt)
* [Hide-UDModal](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Hide-UDModal.txt)
