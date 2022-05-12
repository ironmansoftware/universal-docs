---
description: Stack components in one dimesion.
---

# Stack

The Stack component manages layout of immediate children along the vertical or horizontal axis with optional spacing and/or dividers between each child.

## Horizontal Stack

Horizontally stacked items.&#x20;

![](<../../../../.gitbook/assets/image (314) (2).png>)

```powershell
New-UDStack -Content {
   New-UDPaper -Content { "Item 1" } -Elevation 3
   New-UDPaper -Content { "Item 2" } -Elevation 3
   New-UDPaper -Content { "Item 3" } -Elevation 3
} -Spacing 2
```

## Vertical Stack

Vertically stacked items.&#x20;

![](<../../../../.gitbook/assets/image (348) (1).png>)

```powershell
New-UDStack -Content {
   New-UDPaper -Content { "Item 1" } -Elevation 3
   New-UDPaper -Content { "Item 2" } -Elevation 3
   New-UDPaper -Content { "Item 3" } -Elevation 3
} -Spacing 2 -Direction 'column'
```

## API

* New-UDStack
