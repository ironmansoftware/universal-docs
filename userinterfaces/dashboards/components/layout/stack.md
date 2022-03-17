---
description: Stack components in one dimesion.
---

# Stack

The Stack component manages layout of immediate children along the vertical or horizontal axis with optional spacing and/or dividers between each child.

## Horizontal Stack

Horizontally stacked items.&#x20;

```powershell
New-UDStack -Content {
   New-UDPaper -Content { "Item 1" }
   New-UDPaper -Content { "Item 1" }
   New-UDPaper -Content { "Item 1" }
} -Spacing 2
```

## Vertical Stack

Vertically stacked items.&#x20;

```powershell
New-UDStack -Content {
   New-UDPaper -Content { "Item 1" }
   New-UDPaper -Content { "Item 1" }
   New-UDPaper -Content { "Item 1" }
} -Spacing 2 -Orientation 'column'
```
