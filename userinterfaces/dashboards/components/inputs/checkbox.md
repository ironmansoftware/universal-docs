---
description: Check component for Universal Dashboard
---

# Checkbox

Checkboxes allow the user to select one or more items from a set.

## Checkboxes

![](<../../../../.gitbook/assets/image (41).png>)

Checkboxes can be disabled and checked by default

```powershell
New-UDCheckBox
New-UDCheckBox -Disabled
New-UDCheckBox -Checked $true
New-UDCheckBox -Checked $true -Disabled
```

## Checkboxes with custom icon

![](<../../../../.gitbook/assets/image (68).png>)

Create checkboxes that use any icon and style.

```powershell
$Icon = New-UDIcon -Icon angry -Size lg -Regular
$CheckedIcon = New-UDIcon -Icon angry -Size lg
New-UDCheckBox -Icon $Icon -CheckedIcon $CheckedIcon -Style @{color = '#2196f3'}
```

## Checkboxes with onChange script block

Create checkboxes that fire script blocks when changed.

```powershell
New-UDCheckBox -OnChange {
    Show-UDToast -Title 'Checkbox' -Message $Body
}
```

## Checkbox with custom label placement

![](<../../../../.gitbook/assets/image (38).png>)

You can adjust where the label for the checkbox is placed.

```powershell
New-UDCheckBox -Label 'Demo' -LabelPlacement start
New-UDCheckBox -Label 'Demo' -LabelPlacement top
New-UDCheckBox -Label 'Demo' -LabelPlacement bottom
New-UDCheckBox -Label 'Demo' -LabelPlacement end
```

## Get the value of a Checkbox

You can use `Get-UDElement` to get the value of the checkbox. `Get-UDElement` will also return other properties of the checkbox component.

The following example shows a toast message with the value of the checkbox.

```powershell
New-UDCheckbox -Id 'MyCheckbox' 

New-UDButton -Text 'Get Value' -OnClick {
    Show-UDToast -Message (Get-UDElement -Id 'MyCheckbox').checked
}
```

## API

* [New-UDCheckbox](../../../../cmdlets/New-UDCheckBox.txt)
