---
description: Drawer component for Universal Dashboard
---

# Drawer

{% hint style="warning" %}
This documentation is for the prelease version of PowerShell Universal. You can download pre-release versions on our [Downloads page](https://ironmansoftware.com/downloads).
{% endhint %}

## Permanent Drawer

A permanent drawer will be shown at all times. By default, it is show on the left side of the screen.

```text
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

![Permanent Drawer](../../../.gitbook/assets/image%20%28137%29.png)

