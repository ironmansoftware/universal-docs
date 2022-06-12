---
description: Forms that can be invoked to call scripts and APIs.
---

# Form

## Invoke a Script with a Form

Forms can be used to invoke scripts. The form component ties directly into the automation features to allow for the display of output, progress and respond to feedback.&#x20;

To invoke a script, select the target of Script and the script you'd like to invoke.&#x20;

![](<../../.gitbook/assets/image (248).png>)

By default, no output or progress will be shown. The form will simply consist of a Save button.&#x20;

![](<../../.gitbook/assets/image (249).png>)

If the script succeeds, you'll see a success result. If it fails, it will return a failure result.&#x20;

![](<../../.gitbook/assets/image (250).png>)

### Viewing Output

You can view the output as the script runs by using the Show Output check box.&#x20;

![](<../../.gitbook/assets/image (251).png>)

### Viewing Progress

To view the output of cmdlets like `Write-Progress`, you can use the Show Progress check box. While the script executes, you'll see the progress messages.&#x20;

![](<../../.gitbook/assets/image (252).png>)

The script in this example simply shows progress.&#x20;

```
1..10 | % { 
    Write-Progress -Activity "Processing..." -PercentComplete ($_ * 10)
    Start-Sleep 1
}
```

### Viewing Output after the script has run

To view the output of the script after it has run, you can use the Result Type drop down. The Text result type, will display output as text.&#x20;

![](<../../.gitbook/assets/image (253).png>)

To view output as a table, select the result type of Table.

![](<../../.gitbook/assets/image (254).png>)

### Responding to Feedback

Scripts that request feedback will prompt the user to enter more information.&#x20;

![](<../../.gitbook/assets/image (255).png>)

An example of a script that may request feedback is one that uses `Read-Host`

```
Read-Host "Enter some feedback"
```



## Invoke an API with a Form

Invoking an API with a form can be done by selecting API from the Target Type and then selecting the API endpoint you wish to call.&#x20;

![](<../../.gitbook/assets/image (256).png>)

API endpoints do not support progress, feedback, or output while running the API. They do support returning results as text or tables. APIs that return 200 will show a Success result and other status codes will return Failure.&#x20;

Fields provided to an API endpoint will be sent as a single JSON object with properties for each field.&#x20;

For example, if you had a form with a field named txtName and txtLastName, you could access those properties by deserializing the `$Body` variable.

```
$Fields = $Body | ConvertFrom-Json
$Fields.txtName
$Fields.txtLastName
```

## Fields&#x20;

You can specify fields for each form. Currently forms support text boxes, checkboxes and hidden values. Fields can have a tooltip description and marked as required.&#x20;

![](<../../.gitbook/assets/image (257).png>)

### Fields in Scripts

Fields are provided to scripts as parameters. You can use a `param` block to capture these field values.&#x20;

For example, if you had a FirstName and LastName field, you would define the following param block in your script.&#x20;

```
param(
    $FirstName,
    $LastName
)
```

### Fields in APIs

Fields are provided to APIs as a JSON body to the POST endpoint. Each field will be a property of the JSON object passed to the API.&#x20;

```
$Fields = $Body | ConvertFrom-Json
$Fields.FirstName
$Fields.LastName
```

### Field Types

#### Checkbox

The checkbox field provides a checkbox the user can select and `$true` or `$false` will be sent to the target.&#x20;

**Date**

Allows the user to select a date. The value will be passed as a string.&#x20;

#### Hidden

Hidden fields provide a value to the target that is not shown to the user. The value will be a string.

**Number**

Allows the user to select a number. The value will be passed as an integer.&#x20;

**Password**

{% hint style="info" %}
Available in PowerShell Universal 2.5 or later
{% endhint %}

A textbox with a mask to prevent you from seeing the characters typed.&#x20;

**Select**

Allows the user to select an option from a drop down. The value will be passed as a string.&#x20;

**Switch**

Allows the user to provide a true or false. The value will be passed as a boolean.&#x20;

#### Textbox

The textbox field allows the user to enter any text into the field and it will be submitted to the target. The value will be a string.&#x20;

Time

Allows the user to select a time. The value is passed as a string.&#x20;

**Rating**

Allows the user to select a rating between 0 and 5. The value is passed as a float.&#x20;

## Text

You can customize the text of numerous features of a field including the success and failure text, waiting on feedback text and button text.&#x20;

![](<../../.gitbook/assets/image (258).png>)

## Validation

{% hint style="info" %}
Available in PowerShell Universal 2.9 or later.&#x20;
{% endhint %}

![](<../../.gitbook/assets/image (329).png>)

You can validate a form by selecting an API endpoint from the Validation API field. The validation endpoint must be a POST method. Use the `New-PSUValidationResult` parameter to return whether the validation is successful.&#x20;

![Validation API](<../../.gitbook/assets/image (405).png>)

```powershell
$Fields = $Body | ConvertFrom-Json
if ($Fields.Name -eq 'Adam')
{
     New-PSUValidationResult -Success
}
else 
{
     New-PSUValidationResult -ErrorMessage 'Incorrect name'
}
```

## Smart Properties

Smart properties are hashtables included in the data returned from APIs and Scripts. Tables will automatically translate these hashtables to rendered components when displaying them.

### Links

You can include links by using a hashtable with the `link` type and providing a `url` and `text` property.&#x20;

```powershell
@{
    column = @{
       type = "link"
       url = "https://ironmansoftware.com"
       text = "Ironman Software"
    }
}
```

### Images

You can include images by using a hashtable with the `image` type and specifying any valid `img` HTML attributes.&#x20;

```powershell
@{
    column = @{
       type = "image"
       src = "https://ironmansoftware.com/logo.png"
       height = "10px"
    }
}
```
