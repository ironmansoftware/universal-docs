---
description: Textbox component for Universal Dashboard
---

# Textbox

A textbox lets users enter and edit text.

## Textbox

![](<../../../../.gitbook/assets/image (53).png>)

```powershell
New-UDTextbox -Label 'Standard' -Placeholder 'Textbox'
New-UDTextbox -Label 'Disabled' -Placeholder 'Textbox' -Disabled
New-UDTextbox -Label 'Textbox' -Value 'With value'
```

## Password Textbox

A password textbox will mask the input.

![](<../../../../.gitbook/assets/image (54).png>)

```powershell
New-UDTextbox -Label 'Password' -Type password
```

## Multiline

You can create a multiline textbox by using the `-Multiline` parameter. Pressing enter will add a new line. You can define the number of rows and the max number of rows using `-Rows` and `-RowsMax`.

```powershell
New-UDTextbox -Multiline -Rows 4 -RowsMax 10
```

## Interaction

### Retrieving a textbox value

You can use `Get-UDElement` to get the value of a textbox

```powershell
New-UDTextbox -Id 'txtExample' 
New-UDButton -OnClick {
    $Value = (Get-UDElement -Id 'txtExample').value 
    Show-UDToast -Message $Value
} -Text "Get textbox value"
```

### Setting the textbox value

```powershell
New-UDTextbox -Id 'txtExample' -Label 'Label' -Value 'Value'

New-UDButton -OnClick {

    Set-UDElement -Id 'txtExample' -Properties @{
        Value = "test123"
    }

} -Text "Get textbox value"
```

## Icons

You can set the icon of a textbox by using the `-Icon` parameter and the `New-UDIcon` cmdlet.

```powershell
New-UDTextbox -Id "ServerGroups" -Icon (New-UDIcon -Icon 'server') -Value "This is my server"
```

![](<../../../../.gitbook/assets/image (103).png>)

## Mask

The textbox mask is accomplished using react-imask. You can specify RegEx and pattern matching.&#x20;

* [Pattern Mask](https://imask.js.org/guide.html#masked-pattern)
* [RegEx Mask](https://imask.js.org/guide.html#masked-base)

This example creates a mask for US based phone numbers.

```powershell
New-UDTextbox -Mask "+1 (000) 000-0000"
```

![](<../../../../.gitbook/assets/image (165).png>)

### Unmasking&#x20;

The default behavior of `-Mask` is to return the masked value in forms and `Get-UDElement`. You can return the unmasked value by specifying the `-Unmask` parameter.&#x20;

```powershell
New-UDTextbox -Mask "+1 (000) 000-0000" -Unmask
```

## OnEnter

The `-OnEnter` event handler is executed when the user presses enter in the text field. It is useful for performing other actions, like clicking a button, on enter.&#x20;

```powershell
New-UDTextbox -OnEnter {
    Invoke-UDEndpoint -Id 'submit'
}

New-UDButton -Id 'submit' -OnClick {
    Show-UDToast -Message 'From Textbox'
}
```

## OnBlur

The `-OnBlur` event handler is executed when the textbox loses focus.&#x20;

```powershell
New-UDTextbox -OnBlur {
    Show-UDToast "Blurred"
}
```

## API

[New-UDTextbox](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDTextbox.txt)
