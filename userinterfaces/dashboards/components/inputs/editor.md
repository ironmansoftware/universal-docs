---
description: A text editor component for Universal Dashboard.
---

# Editor

{% hint style="info" %}
Available in PowerShell Universal 2.5 or later.
{% endhint %}

The editor component is available in the `UniversalDashboard.Editor` component library. You will have to add it to your dashboard to be able to use the editor component.&#x20;

The editor component is based on [Editor.js](https://editorjs.io). It's a block editor that accepts text, links, lists, code and images.&#x20;

When working with the editor, you can receive data about the current document via the `OnChange` parameter. By default, data is returned in the Editor.js [JSON format](https://editorjs.io/saving-data).

## Creating an Editor

To create a basic editor, use the `New-UDEditor` cmdlet.

```
New-UDEditor
```

The editor will be available and you can add new blocks by clicking the plus button.&#x20;

![](<../../../../.gitbook/assets/image (307) (1) (1) (1) (1) (1) (1).png>)

## Working with Data

If you define a script block for the `-OnChange` event handler. The `$EventData` variable will contain the current status of the editor. By default, this returns the Editor.JS [JSON block format](https://editorjs.io/saving-data).&#x20;

```
New-UDEditor -OnChange {
    Show-UDToast $EventData
}
```

You can also use the HTML render plugin by specifying the `-Format` parameter.&#x20;

```
New-UDEditor -OnChange {
    Show-UDToast $EventData
} -Format 'html'
```

To specify the default data for the editor, use the `-Data` parameter. You need to specify the JSON block format.&#x20;

```
New-UDEditor -Data $Data
```

## API

### New-UDEditor

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td>Id</td><td>string</td><td>The ID of this component.</td><td>false</td></tr><tr><td>Data</td><td>Hashtable</td><td>The Editor.JS data for this component</td><td>false</td></tr><tr><td>OnChange</td><td>ScriptBlock</td><td>The script block event handler to call when the editor data changes.</td><td>false</td></tr><tr><td>Format</td><td>string</td><td>Whether to return either json or html in the OnChange script block.</td><td>false</td></tr></tbody></table>
