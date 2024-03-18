---
description: Button component for Universal Apps
---

# Button

Buttons allow users to take actions, and make choices, with a single tap.

## Contained Button

![](<../../../.gitbook/assets/image (55).png>)

Contained buttons are high-emphasis, distinguished by their use of elevation and fill. They contain actions that are primary to your app.

```powershell
 New-UDButton -Variant 'contained' -Text 'Default'
```

## Outlined Button

![](<../../../.gitbook/assets/image (315).png>)

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

![](<../../../.gitbook/assets/image (537).png>)

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

## Loading Button

![](<../../../.gitbook/assets/image (117).png>)

Loading buttons will display a loading icon while an event handler is running. This is useful for longer running events.

```powershell
New-UDButton -Text 'Message Box' -OnClick {
    Show-UDToast -Message 'Hello, world!'
    Start-Sleep 10
} -ShowLoading
```

## Button Group

A button group produces a button with a drop down menu. This is also referred to a split button.

```powershell
New-UDButtonGroup -Children {
    New-UDButtonGroupItem -Text "Button 1" -OnClick {
        Show-UDToast "Button 1"
    }
    New-UDButtonGroupItem -Text "Button 2" -OnClick {
        Show-UDToast "Button 2"
    }
    New-UDButtonGroupItem -Text "Button 3" -OnClick {
        Show-UDToast "Button 3"
    }
}
```

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Button Group</p></figcaption></figure>

## Disable Button After Click

This example uses `Set-UDElement` to disable the button after performing an action.&#x20;

```powershell
New-UDButton -Id "btn1" -OnClick {
    Show-UDToast "Hello!"
    Set-UDElement -Id 'btn1' -Attributes @{
        disabled = $true
    }
}
```

## API

* [New-UDButton](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDButton.txt)
