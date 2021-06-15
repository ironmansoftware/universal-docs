---
description: Switch component for Universal Dashboard
---

# Switch

Switches toggle the state of a single setting on or off.

Switches are the preferred way to adjust settings on mobile. The option that the switch controls, as well as the state it’s in, should be made clear from the corresponding inline label.

## Switch

Create a basic switch.

![](../../../.gitbook/assets/image%20%2870%29.png)

```text
New-UDSwitch -Checked $true 
New-UDSwitch -Checked $true -Disabled
```

## OnChange Event

Respond to when a switch value is changed. The `$EventData` variable will include whether or not the switch was checked or unchecked.

```text
New-UDSwitch -OnChange { Show-UDToast -Message $EventData }
```

## Get-UDElement Support

You can retrieve the value of the switch within another component by using `Get-UDElement`. Use the Checked property to determine whether the switch is checked out not.

```text
New-UDSwitch -Id 'switch' 
New-UDButton -Text 'Click' -OnClick {
    Show-UDToast -Message (Get-UDElement -Id 'switch').checked
}
```

**New-UDSwitch**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Disabled | SwitchParameter | Whether this switch is disabled. | false |
| OnChange | Endpoint | A script block that is called when this switch changes. The $EventData variable will contain the checked value \($true$false\). | false |
| Checked | Boolean | Whether this switch is checked. | false |

