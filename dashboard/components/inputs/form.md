---
description: Form component for Universal Dashboard
---

# Form

Forms provide a way to collect data from users.

Forms can include any type of control you want. This allows you to customize the look and feel and use any input controls.

Data entered via the input controls will be sent back to the the OnSubmit script block when the form is submitted.

## Supported Controls

The following input controls automatically integrate with a form. The values that are set within these controls will be sent during validation and in the OnSubmit event handler. 

* [Autocomplete](automcomplete.md)
* [Checkbox](checkbox.md)
* [Date Picker](date-picker.md)
* [Radio](radio.md)
* [Select](select.md)
* [Slider](slider.md)
* [Switch](switch.md)
* [Textbox](textbox.md)
* [Time Picker](time-picker.md)

## Simple Form

Simple forms can use inputs like text boxes and checkboxes.

```text
New-UDForm -Content {
    New-UDTextbox -Id 'txtTextfield'
    New-UDCheckbox -Id 'chkCheckbox'
} -OnSubmit {
    Show-UDToast -Message $Body
}
```

## Formatting a Form

Since forms can use any component, you can use standard formatting components within the form.

```text
New-UDForm -Content {

    New-UDRow -Columns {
        New-UDColumn -SmallSize 6 -LargeSize 6 -Content {
            New-UDTextbox -Id 'txtTextfield' -Label 'First Name' 
        }
        New-UDColumn -SmallSize 6 -LargeSize 6 -Content {
            New-UDTextbox -Id 'txtTextfield' -Label 'Last Name'
        }
    }

    New-UDTextbox -Id 'txtAddress' -Label 'Address'

    New-UDRow -Columns {
        New-UDColumn -SmallSize 6 -LargeSize 6  -Content {
            New-UDTextbox -Id 'txtState' -Label 'State'
        }
        New-UDColumn -SmallSize 6 -LargeSize 6  -Content {
            New-UDTextbox -Id 'txtZipCode' -Label 'ZIP Code'
        }
    }

} -OnSubmit {
    Show-UDToast -Message $Body
}
```

## Validating a Form

Form validation can be accomplished by using the OnValidate script block parameter

```text
New-UDForm -Content {
    New-UDTextbox -Id 'txtValidateForm'
} -OnValidate {
    $FormContent = $Body | ConvertFrom-Json 

    if ($FormContent.txtValidateForm -eq $null -or $FormContent.txtValidateForm -eq '') {
        New-UDFormValidationResult -ValidationError "txtValidateForm is required"
    } else {
        New-UDFormValidationResult -Valid
    }
} -OnSubmit {
    Show-UDToast -Message $Body
}
```

