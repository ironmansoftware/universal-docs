---
description: Form component for Universal Dashboard
---

# Form

{% embed url="https://youtu.be/o8Bl1NsCc2Y" %}

Forms provide a way to collect data from users.

Forms can include any type of control you want. This allows you to customize the look and feel and use any input controls.

Data entered via the input controls will be sent back to the the `OnSubmit` script block when the form is submitted. Within the `OnSubmit` event handler, you will access to the `$EventData` variable that will contain properties for each of the fields in the form.

For example, if you have two fields, you will have two properties on `$EventData`.

```powershell
New-UDForm -Content {
    New-UDTextbox -Id 'txtTextField'
    New-UDCheckbox -Id 'chkCheckbox'
} -OnSubmit {
    Show-UDToast -Message $EventData.txtTextField
    Show-UDToast -Message $EventData.chkCheckbox
}
```

## Supported Controls

The following input controls automatically integrate with a form. The values that are set within these controls will be sent during validation and in the `OnSubmit` event handler.

* [Autocomplete](automcomplete.md)
* [Checkbox](checkbox.md)
* [Date Picker](date-picker.md)
* [Radio](radio.md)
* [Select](select.md)
* [Slider](slider.md)
* [Switch](switch.md)
* [Textbox](textbox.md)
* [Time Picker](time-picker.md)
* [Transfer List](transfer-list.md)
* [Upload](upload.md)

## Simple Form

![](<../../../../.gitbook/assets/image (41).png>)

Simple forms can use inputs like text boxes and checkboxes.

```powershell
New-UDForm -Content {
    New-UDTextbox -Id 'txtTextfield'
    New-UDCheckbox -Id 'chkCheckbox'
} -OnSubmit {
    Show-UDToast -Message $EventData.txtTextfield
    Show-UDToast -Message $EventData.chkCheckbox
}
```

## Formatting a Form

![](<../../../../.gitbook/assets/image (42).png>)

Since forms can use any component, you can use standard formatting components within the form.

```powershell
New-UDForm -Content {

    New-UDRow -Columns {
        New-UDColumn -SmallSize 6 -LargeSize 6 -Content {
            New-UDTextbox -Id 'txtFirstName' -Label 'First Name' 
        }
        New-UDColumn -SmallSize 6 -LargeSize 6 -Content {
            New-UDTextbox -Id 'txtLastName' -Label 'Last Name'
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
    Show-UDToast -Message $EventData.txtFirstName
    Show-UDToast -Message $EventData.txtLastName
}
```

## Returning Components

When a form is submitted, you can optionally return another component to replace the form on the page. You can return any Universal Dashboard component. All you need to do is ensure that the component is written to the pipeline within the `OnSubmit` event handler.

```powershell
New-UDForm -Content {
    New-UDTextbox -Id 'txtTextfield'
} -OnSubmit {
    New-UDTypography -Text $EventData.txtTextfield
}
```

## Validating a Form

Form validation can be accomplished by using the OnValidate script block parameter

```powershell
New-UDForm -Content {
    New-UDTextbox -Id 'txtValidateForm'
} -OnValidate {
    $FormContent = $EventData

    if ($FormContent.txtValidateForm -eq $null -or $FormContent.txtValidateForm -eq '') {
        New-UDFormValidationResult -ValidationError "txtValidateForm is required"
    } else {
        New-UDFormValidationResult -Valid
    }
} -OnSubmit {
    Show-UDToast -Message $Body
}
```

## Canceling a Form

You can define an `-OnCancel` event handler to invoke when the cancel button is pressed. This can be used to take actions like close a modal.

```powershell
New-UDButton -Text 'On Form' -OnClick {
    Show-UDModal -Content {
        New-UDForm -Content {
            New-UDTextbox -Label 'Hello'
        } -OnSubmit {
            Show-UDToast -Message 'Submitted!'
            Hide-UDModal
        } -OnCancel {
            Hide-UDModal
        }
    }
}
```

## Displaying output without Replacing the form

Although you can return components directly from a form, you may want to retain the form so users can input data again. To do so, you can use `Set-UDElement` and a placeholder element that you can set the content to.

In this example, we have an empty form that, when submitted, will update the `results` element with a UDCard.

```powershell
New-UDForm -Content {

} -OnSubmit {
   Set-UDElement -Id 'results' -Content {
      New-UDCard -Content { "Hello " + (Get-Date) }
   }
}

New-UDElement -Id 'results' -Tag 'div'
```

## API

* [New-UDForm](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDForm.txt)
* [New-UDFormValidationResult](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDValidationResult.txt)
