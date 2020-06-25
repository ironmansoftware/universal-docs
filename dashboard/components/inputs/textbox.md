---
description: Textbox component for Universal Dashboard
---

# Textbox

A textbox lets users enter and edit text.

## Textbox

![](../../../.gitbook/assets/image%20%2847%29.png)

```text
New-UDTextbox -Label 'Standard' -Placeholder 'Textbox'
New-UDTextbox -Label 'Disabled' -Placeholder 'Textbox' -Disabled
New-UDTextbox -Label 'Textbox' -Value 'With value'
```

## Password Textbox

![](../../../.gitbook/assets/image%20%2855%29.png)

```text
New-UDTextbox -Label 'Password' -Type password
```

## Retrieving a textbox value

You can use Get-UDElement to get the value of a textbox

```text
New-UDTextbox -Id 'txtExample' 
New-UDButton -OnClick {
    $Value = (Get-UDElement -Id 'txtExample').value 
    Show-UDToast -Message $Value
} -Text "Get textbox value"
```



**New-UDTextbox**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Label | String | A label to show above this textbox. | false |
| Placeholder | String | A placeholder to place within the text box. | false |
| Value | Object | The current value of the textbox. | false |
| Type | String | The type of textbox. This can be values such as text, password or email. | false |
| Disabled | SwitchParameter | Whether this textbox is disabled. | false |
| Icon | Object | The icon to show next to the textbox. | false |
| Autofocus | SwitchParameter | Whether to autofocus this textbox. | false |

