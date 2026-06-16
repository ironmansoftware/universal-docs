---
description: A text editor component for Universal Apps.
---

# Editor

The editor component is based on [Editor.js](https://editorjs.io/). It's a block editor that accepts text, links, lists, code and images.

When working with the editor, you can receive data about the current document via the `OnChange` parameter. By default, data is returned in the Editor.js [JSON format](https://editorjs.io/saving-data).

## Creating an Editor

To create a basic editor, use the `New-UDEditor` cmdlet.

```
New-UDEditor
```

The editor will be available and you can add new blocks by clicking the plus button.

![](<../../../.gitbook/assets/image (262).png>)

## Working with Data

If you define a script block for the `-OnChange` event handler. The `$EventData` variable will contain the current status of the editor. By default, this returns the Editor.JS [JSON block format](https://editorjs.io/saving-data).

```
New-UDEditor -OnChange {
    Show-UDToast $EventData
}
```

You can also use the HTML render plugin by specifying the `-Format` parameter.

```
New-UDEditor -OnChange {
    Show-UDToast $EventData
} -Format 'html'
```

To specify the default data for the editor, use the `-Data` parameter. You must provide a hashtable formatted as an Editor.JS JSON block object.

{% hint style="info" %}
Even if `-Format html` is specified, the `-Data` parameter always requires the default data to follow the Editor.JS JSON block object structure (e.g., a hashtable with a `blocks` array), not a raw HTML string.
{% endhint %}

```powershell
$Data = @{
    blocks = @(
        @{
            type = "paragraph"
            data = @{
                text = "Default Text"
            }
        }
    )
}

New-UDEditor -Data $Data
```

## Image Support

In order to support images, you will need to provide a [published folder](../../../platform/published-folders.md) in which to upload the images. Once a published folder is defined, images can be uploaded directly in the editor. They will be placed within the directory and then served through the request path.

```powershell
New-UDEditor -PublishedFolder 'MyImages'
```

## API

### New-UDEditor

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td>Id</td><td>string</td><td>The ID of this component.</td><td>false</td></tr><tr><td>Data</td><td>Hashtable</td><td>The Editor.JS data for this component</td><td>false</td></tr><tr><td>OnChange</td><td>ScriptBlock</td><td>The script block event handler to call when the editor data changes.</td><td>false</td></tr><tr><td>Format</td><td>string</td><td>Whether to return either json or html in the OnChange script block.</td><td>false</td></tr></tbody></table>
