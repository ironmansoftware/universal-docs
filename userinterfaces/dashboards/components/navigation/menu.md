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

```
New-UDMenu -Content {
   New-UDMenuItem -Text 'Item 1'
   New-UDMenuItem -Text 'Item 1'
   New-UDMenuItem -Text 'Item 1'
}
```

![](<../../../../.gitbook/assets/image (303).png>)

## Button Styles

You can edit the style of the menu by adjusting the variant parameter.&#x20;

```
New-UDMenu -Content {
   New-UDMenuItem -Text 'Item 1'
   New-UDMenuItem -Text 'Item 1'
   New-UDMenuItem -Text 'Item 1'
} -Variant outlined
```

## Values

You can use the value parameter to define a value that differs from the text displayed.&#x20;

```
New-UDMenu -Content {
   New-UDMenuItem -Text 'Item 1' -Value 'item1'
   New-UDMenuItem -Text 'Item 1' -Value 'item2'
   New-UDMenuItem -Text 'Item 1' -Value 'item3'
}
```

## OnChange Event Handler

Use the `-OnChange` parameter to specify a script block to call when a new value is selected.  The value of the selected item will be available in `$EventData`.

```
New-UDMenu -Text 'Click Me' -OnChange {
    Show-UDToast $EventData
} -Children {
    New-UDMenuItem -Text 'Test'
    New-UDMenuItem -Text 'Test2'
    New-UDMenuItem -Text 'Test3'
}
```

## API

### New-UDMenu

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td>Id</td><td>string</td><td>The ID of this component.</td><td>false</td></tr><tr><td>Text</td><td>string</td><td>The text to display in the button that opens this menu.</td><td>true</td></tr><tr><td>OnChange</td><td>ScriptBlock</td><td></td><td>true</td></tr><tr><td>Children</td><td>ScriptBlock</td><td>Items to display in the menu.</td><td>true</td></tr><tr><td>ClassName</td><td>string</td><td>A CSS class to apply to the element</td><td>false</td></tr><tr><td>Variant</td><td>string</td><td>Style of the menu button: text, outlined, contained</td><td>false</td></tr></tbody></table>

### New-UDMenuItem

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td>Text</td><td>string</td><td>The text to display in the menu item.</td><td>true</td></tr><tr><td>Value</td><td>string</td><td>An alternate value to use for this menu item. When not specified. the text is used. </td><td>false</td></tr></tbody></table>
