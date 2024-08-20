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
* Data Visualization&#x20;
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
  * [Stepper ](navigation/stepper.md)
  * [Tabs](navigation/tabs.md)
* Layout
  * [Grid ](layout/grid.md)
  * [Stack](layout/stack.md)
* Utilities
  * [Dynamic](../../portal/portal-widgets/dynamic.md)
  * [Element ](utilities/element.md)
  * [HTML](utilities/html.md)
* Surfaces
  * [Card](surfaces/card.md)
  * [Expansion Panel](surfaces/expansion-panel.md)
