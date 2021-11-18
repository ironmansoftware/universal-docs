---
description: Chip component for Universal Dashboard.
---

# Chip

Chips are compact elements that represent an input, attribute, or action.

Chips allow users to enter information, make selections, filter content, or trigger actions.

While included here as a standalone component, the most common use will be in some form of input, so some of the behavior demonstrated here is not shown in context.

## Basic Chips

![](<../../../../.gitbook/assets/image (71).png>)

```
 New-UDChip -Label 'Basic'
```

## Chips with Icons

![](<../../../../.gitbook/assets/image (43).png>)

```
New-UDChip -Label 'Basic' -Icon (New-UDIcon -Icon 'user')
```

## OnClick

Shows a toast when the chip is clicked.

```
New-UDChip -Label 'OnClick' -OnClick {
    Show-UDToast -Message 'Hello!'
}
```

## OnDelete

```
New-UDChip -Label 'OnDelete' -OnClick {
    Show-UDToast -Message 'Goodbye!'
}
```

## **API**

[New-UDChip](../../../../cmdlets/New-UDChip.txt)
