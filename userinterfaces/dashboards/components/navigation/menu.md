---
description: New-UDMenu component for Universal Dashboard.
---

# Menu

{% hint style="info" %}
Available in PowerShell Universal 2.5 or later.
{% endhint %}

The menu component can be used to provide a drop down list of options for the user to select.&#x20;

## Basic Menu

Create a basic menu.&#x20;

```powershell
New-UDMenu -Content {
   New-UDMenuItem -Text 'Item 1'
   New-UDMenuItem -Text 'Item 1'
   New-UDMenuItem -Text 'Item 1'
}
```

![](<../../../../.gitbook/assets/image (305) (1) (1) (1).png>)

## Button Styles

You can edit the style of the menu by adjusting the variant parameter.&#x20;

```powershell
New-UDMenu -Content {
   New-UDMenuItem -Text 'Item 1'
   New-UDMenuItem -Text 'Item 1'
   New-UDMenuItem -Text 'Item 1'
} -Variant outlined
```

## Values

You can use the value parameter to define a value that differs from the text displayed.&#x20;

```powershell
New-UDMenu -Content {
   New-UDMenuItem -Text 'Item 1' -Value 'item1'
   New-UDMenuItem -Text 'Item 1' -Value 'item2'
   New-UDMenuItem -Text 'Item 1' -Value 'item3'
}
```

## OnChange Event Handler

Use the `-OnChange` parameter to specify a script block to call when a new value is selected.  The value of the selected item will be available in `$EventData`.

```powershell
New-UDMenu -Text 'Click Me' -OnChange {
    Show-UDToast $EventData
} -Children {
    New-UDMenuItem -Text 'Test'
    New-UDMenuItem -Text 'Test2'
    New-UDMenuItem -Text 'Test3'
}
```

## API

* [New-UDMenu](../../../../cmdlets/New-UDMenu.txt)
* [New-UDMenuItem](../../../../cmdlets/New-UDMenuItem.txt)
