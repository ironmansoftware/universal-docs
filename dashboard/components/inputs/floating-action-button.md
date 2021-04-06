---
description: Floating action button component for Universal Dashboard
---

# Floating Action Button

A floating action button \(FAB\) performs the primary, or most common, action on a screen.

A floating action button appears in front of all screen content, typically as a circular shape with an icon in its center. FABs come in two types: regular, and extended.

Only use a FAB if it is the most suitable way to present a screen’s primary action.

Only one floating action button is recommended per screen to represent the most common action.

## Floating Action Button

![](../../../.gitbook/assets/image%20%2842%29.png)

```text
New-UDFloatingActionButton -Icon (New-UDIcon -Icon user) -Size Small
New-UDFloatingActionButton -Icon (New-UDIcon -Icon user) -Size Medium
New-UDFloatingActionButton -Icon (New-UDIcon -Icon user) -Size Large
```

## OnClick

```text
New-UDFloatingActionButton -Icon (New-UDIcon -Icon user) -OnClick {
    Show-UDToast -Message "Hello!"
}
```

**New-UDFloatingActionButton**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Icon | Object | The icon to put within the floating action button. | false |
| Size | Object | The size of the button. | false |
| OnClick | Object | A script block to execute when the floating action button is clicked. | false |

