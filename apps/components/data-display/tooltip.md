---
description: Tooltip component for PowerShell Universal Apps.
---

# Tooltip

Tooltips display informative text when users hover over an element.

## Basic Tooltip

```powershell
New-UDTooltip -Content {
    New-UDIcon -Icon 'User'
} -TooltipContent {
    "User"
}
```

## Placement

Place the tooltip on `top`, `bottom`, `left` or `right`.

```powershell
New-UDTooltip -Content {
    New-UDIcon -Icon 'User'
} -TooltipContent {
    "User"
} -Place 'bottom'
```

## Custom Content

Tooltip content can contain any UD element.&#x20;

```powershell
New-UDTooltip -Content {
    New-UDIcon -Icon 'User'
} -TooltipContent {
    New-UDPaper -Children {
        "User"
    }
}
```

## Tooltip Type

Tooltips can be over various types including: `"dark", "success", "warning", "error", "info", "light"`

```powershell
New-UDTooltip -Content {
    New-UDIcon -Icon 'User'
} -TooltipContent {
    "User"
} -Type 'success'
```
