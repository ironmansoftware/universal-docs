---
description: Forms for portal components.
---

# Forms

Forms can be created using the `Form` component. It can be a mix of various types of input components that bind to a PowerShell class type.

## Basic Form

A basic form requires a PowerShell class definition to define the object used as the model for the form. Below is an example of the script behind this Blazor app. It creates a PowerShell class, sets it to the $Model variable and then defines an event callback to invoke when the form is submitted.&#x20;

```powershell
class MyClass {
    [string]$Str 
}

$Variables["Model"] = [MyClass]::new()

function Submit {
    param($EventArgs)

    $MessageService.Success($EventArgs.Model.Str)
}
```

To use the above PowerShell script in a form, you can use the following PSBlazor syntax.&#x20;

```markup
<Row>
    <Form Model="$Model" OnFinish="Submit">
        <FormItem>
            <Input bind-Value="$Model.Str" />
        </FormItem>
        <FormItem>
            <Button HtmlType="Submit">Submit</Button>
        </FormItem>
    </Form>
</Row>
```
