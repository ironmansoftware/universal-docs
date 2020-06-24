---
description: Chip component for Universal Dashboard.
---

# Chip

Chips are compact elements that represent an input, attribute, or action.

Chips allow users to enter information, make selections, filter content, or trigger actions.

While included here as a standalone component, the most common use will be in some form of input, so some of the behavior demonstrated here is not shown in context.

## Basic Chips

```text
 New-UDChip -Label 'Basic'
```

## Chips with Icons

```text
New-UDChip -Label 'Basic' -Icon (New-UDIcon -Icon 'user')
```

## OnClick

```text
New-UDChip -Label 'OnClick' -OnClick {
    Show-UDToast -Message 'Hello!'
}
```

## OnDelete

```text
New-UDChip -Label 'OnDelete' -OnClick {
    Show-UDToast -Message 'Goodbye!'
}
```

