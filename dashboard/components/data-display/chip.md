---
description: Chip component for Universal Dashboard.
---

# Chip

Chips are compact elements that represent an input, attribute, or action.

Chips allow users to enter information, make selections, filter content, or trigger actions.

While included here as a standalone component, the most common use will be in some form of input, so some of the behavior demonstrated here is not shown in context.

## Basic Chips

![](../../../.gitbook/assets/image%20%2871%29.png)

```PowerShell
 New-UDChip -Label 'Basic'
```

## Chips with Icons

![](../../../.gitbook/assets/image%20%2843%29.png)

```PowerShell
New-UDChip -Label 'Basic' -Icon (New-UDIcon -Icon 'user')
```

## OnClick

Shows a toast when the chip is clicked. 

```PowerShell
New-UDChip -Label 'OnClick' -OnClick {
    Show-UDToast -Message 'Hello!'
}
```

## OnDelete

```PowerShell
New-UDChip -Label 'OnDelete' -OnClick {
    Show-UDToast -Message 'Goodbye!'
}
```



**New-UDChip**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Label | String | The label for the chip. | false |
| OnDelete | Object | A script block to call when the chip is deleted. | false |
| OnClick | Object | A script block to call when the chip is clicked. | false |
| Icon | Object | An icon to show within the chip. | false |
| Style | Hashtable | CSS styles to apply to the chip. | false |
| Variant | String | The theme variant to apply to the chip. | false |
| Avatar | String | An avatar to show within the chip. | false |
| AvatarType | String | The type of avatar to show in the chip. | false |

