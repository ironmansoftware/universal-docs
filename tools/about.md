---
description: Learn about tools built with PowerShell and Blazor.
---

# About

Tools are user interfaces build with PowerShell and Blazor. You can create robust web-based used interfaces with minimal web development experience.&#x20;

## What is PSBlazor Syntax?&#x20;

PSBlazor is a custom XML syntax based on [Blazor](https://learn.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-8.0). PSBlazor allows for declarative interfaces to be built without the need to write HTML or JavaScript. It integrates with PowerShell through data binding, event callbacks to functions and provides access to services provided by PowerShell Universal.&#x20;

An example PSBlazor XML document would look something like this.&#x20;

```markup
<Button OnClick="ClickMe" Icon="user">Title</Button>
```

Alongside the `.razor` file, a `.psm1` module file is also created. This file contains all the logic for the PSBlazor page or component. These module files are standard PowerShell script with variables for accessing and updating the PSBlazor interface.&#x20;

The following example would display a message box in the interface with the text `Ouch!`.&#x20;

```powershell
function ClickMe {
    $MessageService.Error("Ouch!")
}
```

## How are PowerShell and Blazor apps different?&#x20;

PowerShell Apps are built entirely using PowerShell script and typically run within their own process. By using PowerShell script, you can create very customized interfaces that do not require any other languages.&#x20;

Blazor Apps run within the PowerShell Universal server and require PSBlazor pages to be created. They are still interactive and customizable but sacrifice some flexibility for simplicity.&#x20;

Both apps and tools can call APIs and scripts within PowerShell Universal using the built-in `Universal` module.

