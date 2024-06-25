---
description: Information about creating portal components.
---

# Components

Components are user interfaces blocks built with PowerShell and Blazor. You can create robust web-based used interfaces with minimal web development experience.&#x20;

## What is the PSBlazor Syntax?&#x20;

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
