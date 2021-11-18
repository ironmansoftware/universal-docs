---
description: Switch component for Universal Dashboard
---

# Switch

Switches toggle the state of a single setting on or off.

Switches are the preferred way to adjust settings on mobile. The option that the switch controls, as well as the state it’s in, should be made clear from the corresponding inline label.

## Switch

Create a basic switch.

![](<../../../../.gitbook/assets/image (70).png>)

```powershell
New-UDSwitch -Checked $true 
New-UDSwitch -Checked $true -Disabled
```

## OnChange Event

Respond to when a switch value is changed. The `$EventData` variable will include whether or not the switch was checked or unchecked.

```powershell
New-UDSwitch -OnChange { Show-UDToast -Message $EventData }
```

## Get-UDElement Support

You can retrieve the value of the switch within another component by using `Get-UDElement`. Use the Checked property to determine whether the switch is checked out not.

```powershell
New-UDSwitch -Id 'switch' 
New-UDButton -Text 'Click' -OnClick {
    Show-UDToast -Message (Get-UDElement -Id 'switch').checked
}
```

## API

* [New-UDSwitch](../../../../cmdlets/New-UDSwitch.txt)
