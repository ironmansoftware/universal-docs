---
description: Launch PowerShell scripts based on custom protocol handlers.
---

# Protocol Handlers

![Protocol Handlers in the Admin Console](<../.gitbook/assets/image (332).png>)

Protocol handlers allow you to trigger scripts when custom protocols are executed. Protocols can be executed locally and also from webpages as links.&#x20;

## Define a Protocol Handle

You can define protocol handlers in the `protocolHandlers.ps1` file using the `New-PSUProtocolHandler` cmdlet. You will need to define the protocol name and script to execute.&#x20;

```powershell
New-PSUProtocolHandler -Script test.ps1 -Protocol psu
```

To execute the protocol handler, you could include the following HTML tag in a web page.&#x20;

```powershell
<a href="psu://test">Click Me</a>
```

## Accessing URI Data

When a script is executed, you will receive the `$ProtocolUri` parameter. It will include the full URI that was invoked. For example, a script could take the URI and show a page.&#x20;

```powershell
param($ProtocolUri)

$Page = $ProtocolUri.Replace("psu://", "")
$Page
Show-PSUPage -Url $Page
```
