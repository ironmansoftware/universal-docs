---
description: Drawer component for Universal Apps
---

# Drawer

## Permanent Drawer

A permanent drawer will be shown at all times. By default, it is show on the left side of the screen.

```powershell
New-UDDrawer -Variant 'permanent' -Content {
  New-UDList -Children {
        New-UDListItem -Label "Home"
        New-UDListItem -Label "Getting Started" -Children {
            New-UDListItem -Label "Installation" -OnClick {}
            New-UDListItem -Label "Usage" -OnClick {}
            New-UDListItem -Label "FAQs" -OnClick {}
            New-UDListItem -Label "System Requirements" -OnClick {}
            New-UDListItem -Label "Purchasing" -OnClick {}
        }
    }
}
```

![Permanent Drawer](<../../../.gitbook/assets/image (295).png>)

## API&#x20;

* [New-UDDrawer](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDDrawer.txt)

###
