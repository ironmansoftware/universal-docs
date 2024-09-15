---
description: Information about PSBlazor syntax.
---

# Syntax

PSBlazor is a custom syntax based on Blazor and Razor pages. It is similar to XML or XAML and provides a mechanism to declaratively define a user interface.

## Components

Each component is defined with an XML node, such as `<Button>` or `<Text>`. Each component has its own set of attributes that customize the behavior and look and feel of the widget. Some components support child content and can include nested components.

### Defining a Component

To define a component, you will use the PSBlazor code editor to add the component's XML tags. For example, to create a button, you would do the following.

```xml
<Button>Click Me</Button>
```

The result is page with a button defined.

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption><p>Button on a tool</p></figcaption></figure>

### Setting Attributes

Every component has attributes available. Within the code editor for the PSBlazor page, attributes will automatically be listed for the current component you are editing.

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption><p>PSBlazor Attribute Components</p></figcaption></figure>

Setting attributes is the same as setting any XML attribute. This example changes the button to the danger state.

```xml
<Row>
    <Button Danger="true">Click Me</Button>
</Row>
```

Once you save the tool, it will update the display. With the button in danger state, you'll see it is now red.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption><p>Danger button</p></figcaption></figure>

### Child Content

Some components provide the ability to define child content. You can use the `<ChildContent>` node to specify this is the case.

```xml
<Row>
   <ChildContent>
      <Button>Click Me</Button>
   </ChildContent>
</Row>
```

If no other nodes are specified within the child of the component, then it is assumed to be child content. The above can be simplified to this.

```xml
<Row>
    <Button>Click Me</Button>
</Row>
```

Some components provide template attributes that can be set by specifying multiple child content nodes with the appropriate node names. For example, the table can have child content that consists of columns and a title template that defines how the title is displayed. When multiple child nodes are defined, `<ChildContent>` is required.

```xml
<Table DataSource="$Services">
   <ChildContent>
       <PropertyColumn Name="Name" />
   </ChildContent>
   <TitleTemplate>
      <Text>My Services</Text>
   </TitleTemplate>
</Table>
```

## PowerShell

Each PSBlazor tool or component has an associated PSM1 file that contains interactive logic. This logic can interact with modules, invoke scripts in PSU, or update the interface based on data processed by the script.

### Event Callbacks

Event callbacks occur when the user interacts with a PSBlazor component. This can include mouse clicks, form submissions or keyboard input. Event callbacks are just PowerShell functions. The following could be used for when a user clicks a button.

```powershell
function OnClick {
}
```

### Arguments

Most event callbacks provide an object that contains information about the event. For example, mouse events include information like the coordinates of the click. You can access them by providing an `$EventArgs` parameter.

```powershell
function OnClick {
   param($EventArgs)
}
```

### Context

Some components are contextual. For example, a table row or a form item. Context values are passed into the event callback with a `$Context` parameter.

```powershell
function OnClick {
   param($Context)
}
```

## Variables

Variables can be used to update the PSBlazor components with data from PowerShell. Use the `$Variables` dictionary to get and set variables.

```powershell
$Variables["TestVariable"] = "Not Clicked"

function OnClick {
    $Variables["TestVariable"] = "Clicked"
}
```

Within the PSBlazor syntax, you can reference variables similar to how you would in PowerShell.

```xml
<Text>$TestVariable</Text>
<Button OnClick="OnClick">Click Me</Button>
```

You can also use variables in attributes.

```xml
<Alert Message="$TestVariable"></Alert>
<Button OnClick="OnClick">Click Me</Button>
```

Variables can also be complex objects such as `PSCustomObject` or `Hashtable`. If they have properties, you can reference those in the PSBlazor syntax as well.

```xml
<Alert Message="$TestVariable.Name"></Alert>
<Button OnClick="OnClick">Click Me</Button>
```

### Data Binding

Data binding provides a mechanism to update variables without having to call PowerShell script. To define a binding between an attribute on a PSBlazor component, use the `bind-{attribute}` syntax.

For example, you could bind to a `$test` variable for an input box like this.

```xml
<Input bind-Value="$TextValue"></Input>
```

In your PowerShell module, you could then access the variable from the `$Variables` object.

```powershell
$Message.Info($Variables["TextValue"])
```

### Life Cycle

Variables are cleared when a user refreshes the page. They are not cached beyond this scope. Each user and tool page will have a different set of variables.
