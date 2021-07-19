---
description: Drawer component for Universal Dashboard
---

# Drawer

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

## API 

### New-UDDrawer

| Name | Description | Required | Type | Default Value |
| :--- | :--- | :--- | :--- | :--- |
| Id | The ID of this component. | false | string | Guid |
| Children | Children of this drawer. You can use components such as New-UDList within the drawer. | true | ScriptBlock |  |
| Variant | The type of drawer. | false | string \(persistent, permanent, temporary\) | temporary |
| Anchor | Where to anchor the drawer. | false | string \(left, right, top, bottom\) | left |

