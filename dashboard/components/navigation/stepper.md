---
description: Stepper component for Universal Dashboard
---

# Stepper

**Steppers convey progress through numbered steps. It provides a wizard-like workflow.**

Steppers display progress through a sequence of logical and numbered steps. They may also be used for navigation. Steppers may display a transient feedback message after a step is saved. The stepper supports storing input data in the stepper context. It supports the following controls. 

* [Autocomplete](../inputs/automcomplete.md)
* [Checkbox](../inputs/checkbox.md)
* [Date Picker](../inputs/date-picker.md)
* [Radio](../inputs/radio.md)
* [Select](../inputs/select.md)
* [Slider](../inputs/slider.md)
* [Switch](../inputs/switch.md)
* [Textbox](../inputs/textbox.md)
* [Time Picker](../inputs/time-picker.md)
* [Upload](../inputs/upload.md)

## Stepper

![](../../../.gitbook/assets/image%20%2861%29.png)

```text
New-UDStepper -Steps {
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 1" }
        New-UDTextbox -Id 'txtStep1' 
    } -Label "Step 1"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 2" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep2' 
    } -Label "Step 2"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 3" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep3' 
    } -Label "Step 3"
} -OnFinish {
    New-UDTypography -Text 'Nice! You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
}
```

The $Body variable will contain a JSON string that contains the current state of the stepper. You will receive information about the fields that have been defined within the stepper and info about the current step that has been completed. The $Body JSON string will have the following format. 

```text
{
    context: {
        txtStep1: 'value1',
        txtStep2: 'value2',
        txtStep3: 'value3'
    },
    currentStep: 0
}
```

### Validating a Step

You can validate a step in a stepper by specifying the `OnValidateStep` parameter. The script block will receive a $Body variable with JSON that provides information about the current state of the stepper. You will need to return a validation result using `New-UDValidationResult` to specify whether the current step state is valid. 

The JSON payload will have the following format.

```text
{
    context: {
        field1: 'value1' 
    },
    currentStep: 0
}
```

You will have to convert the JSON string to an object to work with in PowerShell and then return the validation result. 

```text
New-UDStepper -Steps {
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 1" }
        New-UDTextbox -Id 'txtStep1' 
    } -Label "Step 1"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 2" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep2' 
    } -Label "Step 2"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 3" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep3' 
    } -Label "Step 3"
} -OnFinish {
    New-UDTypography -Text 'Nice! You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
} -OnValidateStep {
    $Context = ConvertFrom-Json $Body
    if ($Context.CurrentStep -eq 1 -and $Context.Context.txtStep1 -eq 'bad')
    {
        New-UDValidationResult 
    }
    else
    {
        New-UDValidationResult -Valid 
    }
}
```

**New-UDStepper**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| ActiveStep | Int32 | Sets the active step. This should be the index of the step. | false |
| Children | ScriptBlock | The steps for this stepper. Use New-UDStep to create new steps. | true |
| NonLinear | SwitchParameter | Allows the user to progress to steps out of order. | false |
| AlternativeLabel | SwitchParameter | Places the step label under the step number. | false |
| OnFinish | Endpoint | A script block that is executed when the stepper is finished. | true |
| OnValidateStep | Endpoint | A script block that is executed when validating each step. | false |



**New-UDStep**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| OnLoad | Endpoint | The script block that is executed when the step is loaded. The script block will receive the $Body parameter which contains JSON for the current state of the stepper. If you are using form controls, their data will be availalble in the $Body.Context property. | true |
| Label | String | A label for this step. | false |
| Optional | SwitchParameter | Whether this step is optional. | false |

