---
description: Check component for Universal Dashboard
---

# Checkbox

Checkboxes allow the user to select one or more items from a set.

## Checkboxes

Checkboxes can be disabled and checked by default

```text
New-UDCheckBox
New-UDCheckBox -Disabled
New-UDCheckBox -Checked $true
New-UDCheckBox -Checked $true -Disabled
```

## Checkboxes with custom icon

Create checkboxes that use any icon and style.

```text
$Icon = New-UDIcon -Icon angry -Size lg -Regular
$CheckedIcon = New-UDIcon -Icon angry -Size lg
New-UDCheckBox -Icon $Icon -CheckedIcon $CheckedIcon -Style @{color = '#2196f3'}
```

## Checkboxes with onChange script block

Create checkboxes that fire script blocks when changed.

```text
New-UDCheckBox -OnChange {
    Show-UDToast -Title 'Checkbox' -Message $Body
}    
```

## Checkbox with custom label placement

You can adjust where the label for the checkbox is placed.

```text
New-UDCheckBox -Label 'Demo' -LabelPlacement start
New-UDCheckBox -Label 'Demo' -LabelPlacement top
New-UDCheckBox -Label 'Demo' -LabelPlacement bottom
New-UDCheckBox -Label 'Demo' -LabelPlacement end
```

