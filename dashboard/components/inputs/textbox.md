---
description: Textbox component for Universal Dashboard
---

# Textbox

A textbox lets users enter and edit text.

## Textbox

```text
New-UDTextbox -Label 'Standard' -Placeholder 'Textbox'
New-UDTextbox -Label 'Disabled' -Placeholder 'Textbox' -Disabled
New-UDTextbox -Label 'Textbox' -Value 'With value'
```

## Password Textbox

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

