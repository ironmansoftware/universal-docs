---
description: Button component for Universal Dashboard
---

# Button

Buttons allow users to take actions, and make choices, with a single tap.

## Contained Button

![](<../../../../.gitbook/assets/image (75).png>)

Contained buttons are high-emphasis, distinguished by their use of elevation and fill. They contain actions that are primary to your app.

```powershell
 New-UDButton -Variant 'contained' -Text 'Default'
```

## Outlined Button

![](<../../../../.gitbook/assets/image (36).png>)

Outlined buttons are medium-emphasis buttons. They contain actions that are important, but aren’t the primary action in an app.

```powershell
New-UDButton -Variant 'outlined' -Text 'Default'
```

## Control Button Size

You can control the pixel size of a button based on pixel size by using the Style parameter

```powershell
New-UDButton -Id "Submit" -Text "Submit" -Style @{ Width = "150px"; Height = "100px" }
```

## Buttons with icons and label

![](<../../../../.gitbook/assets/image (82).png>)

Sometimes you might want to have icons for certain button to enhance the UX of the application as we recognize logos more easily than plain text. For example, if you have a delete button you can label it with a dustbin icon.

```powershell
New-UDButton -Icon (New-UDIcon -Icon trash) -Text 'Delete'
```

## Buttons with event handlers

You can specify a script block to execute when the button is clicked

```powershell
New-UDButton -Text 'Message Box' -OnClick {
    Show-UDToast -Message 'Hello, world!'
}
```

## API

* [New-UDButton](../../../../cmdlets/New-UDButton.txt)

****
