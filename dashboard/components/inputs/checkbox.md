---
description: Check component for Universal Dashboard
---

# Checkbox

Checkboxes allow the user to select one or more items from a set.

## Checkboxes

![](../../../.gitbook/assets/image%20%2841%29.png)

Checkboxes can be disabled and checked by default

```text
New-UDCheckBox
New-UDCheckBox -Disabled
New-UDCheckBox -Checked $true
New-UDCheckBox -Checked $true -Disabled
```

## Checkboxes with custom icon

![](../../../.gitbook/assets/image%20%2868%29.png)

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

![](../../../.gitbook/assets/image%20%2838%29.png)

You can adjust where the label for the checkbox is placed.

```text
New-UDCheckBox -Label 'Demo' -LabelPlacement start
New-UDCheckBox -Label 'Demo' -LabelPlacement top
New-UDCheckBox -Label 'Demo' -LabelPlacement bottom
New-UDCheckBox -Label 'Demo' -LabelPlacement end
```



**New-UDCheckbox**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Label | String | The label to show next to the checkbox. | false |
| Icon | Object | The icon to show instead of the default icon. | false |
| CheckedIcon | Object | The icon to show instead of the default checked icon. | false |
| OnChange | Endpoint | Called when the value of the checkbox changes. The $EventData variable will have the current value of the checkbox. | false |
| Style | Hashtable | A hashtable of styles to apply to the checkbox. | false |
| Disabled | SwitchParameter | Whether the checkbox is disabled. | false |
| Checked | Boolean | Whether the checkbox is checked. | false |
| ClassName | String | A CSS class to assign to the checkbox. | false |
| LabelPlacement | String | Where to place the label. | false |
| Id | String | The ID of the component. It defaults to a random GUID. | false |

