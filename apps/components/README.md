---
description: Components are the building blocks of a PowerShell Universal app.
---

# Components

A Universal app is composed of components. When building an app, you can simply call the PowerShell cmdlets within your app script to create a new component.

```powershell
New-UDApp -Title 'Dashboard' -Content {
    New-UDTypography -Text 'Hello, world!'
}
```

## Component Types

There are over 50 components that you can use in your apps. Some of the commonly used components include:

* Data Display
  * [Alerts](data-display/alert.md)
  * [Tables](data-display/table.md)
  * [Timeline](data-display/timeline.md)
* Data Visualization
  * [Charts](data-visualization/charts.md)
  * [Maps](data-visualization/map.md)
* Feedback
  * [Modal](feedback/modal.md)
  * [Progress](feedback/progress.md)
* Inputs
  * [Button](inputs/button.md)
  * [Form](inputs/form.md)
  * [Textbox](inputs/textbox.md)
  * [Switch](inputs/switch.md)
* Navigation
  * [Menu](navigation/menu.md)
  * [Stepper](navigation/stepper.md)
  * [Tabs](navigation/tabs.md)
* Layout
  * [Grid](layout/grid.md)
  * [Stack](layout/stack.md)
* Utilities
  * [Dynamic](../../portal/portal-widgets/dynamic.md)
  * [Element](element.md)
  * [HTML](html.md)
* Surfaces
  * [Card](surfaces/card.md)
  * [Expansion Panel](surfaces/expansion-panel.md)

## Event Handlers

Many components provide event handlers for providing interactive functionality. This can be events like clicks, validation, rendering and more. The interactivity of an event handler is implemented using PowerShell script blocks.&#x20;

For example, the below example creates a button that can be clicked that will then show a toast.

```powershell
New-UDButton -Text "Click me!" -OnClick {
    Show-UDToast -Message "Clicked!"
}
```

Within event handlers, you can run any valid PowerShell script. This means you can interact with cmdlets outside of PSU module such as ActiveDirectory or Microsoft.Graph.

### Event Data

Each event handler may provide it's own event data. Components like tables, forms and textboxes return corresponding data about the state of the component. This could be the current data for a row in the table, the values of a form, or the text of a textbox.&#x20;

You can access the event data using the `$EventData` variable. This variable will be different based on the type of component you are using. For example, the `-OnChange` event of `New-UDTextbox` returns a string in `$EventData`.

```powershell
New-UDTextbox -OnChange {
    Show-UDToast -Message $EventData
}
```

This will be different for other controls. For example, a form will return an object that contains properties about the state of the form.&#x20;

```powershell
New-UDForm -Content {
    New-UDTextbox -Id "UserName"
} -OnSubmit {
    Show-UDToast -Message $EventData.UserName
}
```

You can also access the raw string provided to the event handler using the `$Body` variable. This contains a JSON string the defines the `$EventData`.&#x20;

In addition to the `$EventData` variable, you can also use the `$PSUItem` variable to get more information in certain controls that allow for multiple data types. You'll find the PSUItem data type below.

```csharp
public class PsuItem
{
    public string Id { get; set; }
    public string Type { get; set; }
    public string EventId { get; set; }
    public string EventName { get; set; }
    public string EventData { get; set; }
    public string Location { get; set; }
}
```

### Scoping

Understanding event handler scoping is important to ensuring that your apps behave as expected. PowerShell Universal makes an effort to effectively provide all in-scope variables to event handlers.&#x20;

For example, the below would be natural use of a variable in a standard PowerShell script and also works in event handlers.

```powershell
$Variable = 123
New-UDButton -Text "Click Me" -OnClick {
    Show-UDToast -Message $Variable
}
```

Using `$Global:` and `$Script:` scope will not work as expected because every event handler works in its own runspace. PSU manually moves variables around during processing but does not change variables in other scopes.&#x20;

You should use [custom scopes](../custom-variable-scopes.md) to access variables across event handlers.

Additionally, you should avoid trying to inherit `$EventData` within nested event handlers. Although some components do not define their own event data, it should be assumed that the event data will be overwritten in the nested component.&#x20;

```powershell
New-UDTable -Columns @(
    New-UDTableColumn -Property 'Name' -OnRender {
        New-UDButton -Text $EventData.Name -OnClick {
            # $EventData has been replaced by the button and no longer has a name property
            Show-UDToast -Message $EventData.Name
        }
    }
) -Data $Data
```

To avoid this issue, you should store data in another variable to be sent into the nested component's event handler scope.&#x20;

```powershell
New-UDTable -Columns @(
    New-UDTableColumn -Property 'Name' -OnRender {
        $Name = $EventData.Name
        New-UDButton -Text $EventData.Name -OnClick {
            Show-UDToast -Message $Name
        }
    }
) -Data $Data
```
