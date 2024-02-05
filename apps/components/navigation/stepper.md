---
description: Stepper component for Universal Apps
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

![](<../../../.gitbook/assets/image (143).png>)

```powershell
New-UDStepper -Steps {
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 1" }
        New-UDTextbox -Id 'txtStep1' -Value $EventData.Context.txtStep1
    } -Label "Step 1"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 2" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep2' -Value $EventData.Context.txtStep2
    } -Label "Step 2"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 3" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep3' -Value $EventData.Context.txtStep3
    } -Label "Step 3"
} -OnFinish {
    New-UDTypography -Text 'Nice! You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
}
```

The $Body variable will contain a JSON string that contains the current state of the stepper. You will receive information about the fields that have been defined within the stepper and info about the current step that has been completed. The $Body JSON string will have the following format.

```javascript
{
    context: {
        txtStep1: "value1",
        txtStep2: "value2",
        txtStep3: "value3"
    },
    currentStep: 0
}
```

## Validating a Step

You can validate a step in a stepper by specifying the `OnValidateStep` parameter. The script block will receive a $Body variable with JSON that provides information about the current state of the stepper. You will need to return a validation result using `New-UDValidationResult` to specify whether the current step state is valid.

The JSON payload will have the following format. Note that steps are 0 indexed. If you want to validate the first step, check to make sure the step is 0.

```javascript
{
    context: {
        field1: "value1" 
    },
    currentStep: 0
}
```

You will have to convert the JSON string to an object to work with in PowerShell and then return the validation result.

```powershell
New-UDStepper -Steps {
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 1" }
        New-UDTextbox -Id 'txtStep1' -Value $EventData.Context.txtStep1
    } -Label "Step 1"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 2" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep2' -Value $EventData.Context.txtStep2
    } -Label "Step 2"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 3" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep3' -Value $EventData.Context.txtStep3
    } -Label "Step 3"
} -OnFinish {
    New-UDTypography -Text 'Nice! You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
} -OnValidateStep {
    $Context = $EventData
    if ($Context.CurrentStep -eq 0 -and $Context.Context.txtStep1 -eq 'bad')
    {
        New-UDValidationResult 
    }
    else
    {
        New-UDValidationResult -Valid 
    }
}
```

## Skipping Steps

You can direct the user to a particular step in the `OnValidateStep` event handler. Use the `New-UDValidationResult` `-ActiveStep` parameter to move the user to any step after clicking next. Step indices are 0 based.&#x20;

This example moves the user to the last step after completing the first step.&#x20;

```powershell
New-UDStepper -Steps {
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 1" }
        New-UDTextbox -Id 'txtStep1' -Value $EventData.Context.txtStep1
    } -Label "Step 1"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 2" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep2' -Value $EventData.Context.txtStep2
    } -Label "Step 2"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 3" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep3' -Value $EventData.Context.txtStep3
    } -Label "Step 3"
} -OnFinish {
    New-UDTypography -Text 'Nice! You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
} -OnValidateStep {
    $Context = $EventData
    if ($Context.CurrentStep -eq 0 -and $Context.Context.txtStep1 -eq 'bad')
    {
        New-UDValidationResult 
    }
    else
    {
        New-UDValidationResult -Valid -ActiveStep 2
    }
}
```

## Disable Previous Button

You can disable the previous button by using the `-DisablePrevious` parameter of `New-UDValidationResult` .&#x20;

This example disables the previous step whenever the user moves forward in the stepper.

```powershell
New-UDStepper -Steps {
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 1" }
        New-UDTextbox -Id 'txtStep1' -Value $EventData.Context.txtStep1
    } -Label "Step 1"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 2" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep2' -Value $EventData.Context.txtStep2
    } -Label "Step 2"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 3" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep3' -Value $EventData.Context.txtStep3
    } -Label "Step 3"
} -OnFinish {
    New-UDTypography -Text 'Nice! You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
} -OnValidateStep {
    New-UDValidationResult -Valid -DisablePrevious
}
```

## Vertical Steppers

You can create a vertical stepper by setting the `-Orientation` parameter to vertical.

```powershell
New-UDStepper -Steps {
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 1" }
        New-UDTextbox -Id 'txtStep1' -Value $EventData.Context.txtStep1
    } -Label "Step 1"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 2" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep2' -Value $EventData.Context.txtStep2
    } -Label "Step 2"
    New-UDStep -OnLoad {
        New-UDElement -tag 'div' -Content { "Step 3" }
        New-UDElement -tag 'div' -Content { "Previous data: $Body" }
        New-UDTextbox -Id 'txtStep3' -Value $EventData.Context.txtStep3
    } -Label "Step 3"
} -OnFinish {
    New-UDTypography -Text 'Nice! You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
} -Orientation 'vertical'
```

![](<../../../.gitbook/assets/image (311).png>)

## API

* [New-UDStepper](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDStepper.txt)
* [New-UDStep](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDStep.txt)
* [New-UDValidationResult](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDValidationResult.txt)



