---
description: Link component for Universal Dashboard.
---

# Link

Create a hyper link in a dashboard.&#x20;

## Basic Link

Create a basic link that goes to a web page.&#x20;

```powershell
New-UDLink -Text 'Ironman Software' -Url https://www.ironmansoftware.com
```

## Change Style

Adjust the underline and text style.

```powershell
    New-UDLink -Text 'Ironman Software' -Url https://www.ironmansoftware.com -Variant h2 -Underline always
```

## Open in a New Window

Open the link a new window when clicked.&#x20;

```powershell
New-UDLink -Text 'Ironman Software' -Url https://www.ironmansoftware.com -OpenInNewWindow
```

## OnClick Event Handler

Execute a PowerShell script block when the link is clicked.&#x20;

```powershell
New-UDLink -Text 'Ironman Software' -OnClick {
    Show-UDToast "Hello!"
}
```

## API

* [New-UDLink](../../../../cmdlets/New-UDLink.txt)

