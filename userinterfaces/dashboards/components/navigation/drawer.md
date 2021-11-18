---
description: Drawer component for Universal Dashboard
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

![Permanent Drawer](<../../../../.gitbook/assets/image (137).png>)

## API&#x20;

* [New-UDDrawer](../../../../cmdlets/New-UDDrawer.txt)

###
