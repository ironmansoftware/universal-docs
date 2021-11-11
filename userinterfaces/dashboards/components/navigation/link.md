---
description: Link component for Universal Dashboard.
---

# Link

Create a hyper link in a dashboard.&#x20;

## Basic Link

Create a basic link that goes to a web page.&#x20;

```
New-UDLink -Text 'Ironman Software' -Url https://www.ironmansoftware.com
```

## Change Style

Adjust the underline and text style.

```
    New-UDLink -Text 'Ironman Software' -Url https://www.ironmansoftware.com -Variant h2 -Underline always
```

## Open in a New Window

Open the link a new window when clicked.&#x20;

```
New-UDLink -Text 'Ironman Software' -Url https://www.ironmansoftware.com -OpenInNewWindow
```

## OnClick Event Handler

Execute a PowerShell script block when the link is clicked.&#x20;

```
New-UDLink -Text 'Ironman Software' -OnClick {
    Show-UDToast "Hello!"
}
```

## API

### New-UDLink

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td>Id</td><td>string</td><td>The ID of this component</td><td>true</td></tr><tr><td>Url</td><td>string</td><td>The URL to navigate to</td><td>false</td></tr><tr><td>Underline</td><td>string</td><td>The underline behavior: none, hover, always</td><td>false</td></tr><tr><td>Style</td><td>Hashtable</td><td>CSS styles to apply to the link</td><td>false</td></tr><tr><td>Variant</td><td>String</td><td>The variant of text</td><td>false</td></tr><tr><td>ClassName</td><td>String</td><td>The CSS class to apply to the link.</td><td>false</td></tr><tr><td>OpenInNewWindow</td><td>SwitchParameter</td><td>Whether to open the link in a new window.</td><td>false</td></tr><tr><td>Content</td><td>ScriptBlock</td><td>Content to wrap in the link (like a card)</td><td>false</td></tr><tr><td>Text</td><td>string</td><td>Text to display in the link</td><td>false</td></tr><tr><td>OnClick</td><td>ScriptBlock</td><td>A script block to execute when the link is clicked. </td><td>false</td></tr></tbody></table>
