---
description: Form component for Universal Dashboard
---

# Form

Forms provide a way to collect data from users.

Forms can include any type of control you want. This allows you to customize the look and feel and use any input controls.

Data entered via the input controls will be sent back to the the `OnSubmit` script block when the form is submitted. Within the `OnSubmit` event handler, you will access to the `$EventData` variable that will contain properties for each of the fields in the form. 

For example, if you have two fields, you will have two properties on `$EventData`.

```text
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
* [Upload](upload.md)

## Simple Form

![](../../../.gitbook/assets/image%20%2864%29.png)

Simple forms can use inputs like text boxes and checkboxes.

```text
New-UDForm -Content {
    New-UDTextbox -Id 'txtTextfield'
    New-UDCheckbox -Id 'chkCheckbox'
} -OnSubmit {
    Show-UDToast -Message $EventData.txtTextfield
    Show-UDToast -Message $EventData.chkCheckbox
}
```

## Formatting a Form

![](../../../.gitbook/assets/image%20%2849%29.png)

Since forms can use any component, you can use standard formatting components within the form.

```text
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

```text
New-UDForm -Content {
    New-UDTextbox -Id 'txtTextfield'
} -OnSubmit {
    New-UDTypography -Text $EventData.txtTextfield
}
```

## Validating a Form

Form validation can be accomplished by using the OnValidate script block parameter

```text
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

```text
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

**New-UDForm**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Children | ScriptBlock | Controls that make up this form. This can be any combination of controls. Input controls will report their state to the form. | true |
| OnSubmit | Endpoint | A script block that is execute when the form is submitted. You can return controls from this script block and the form will be replaced by the script block. The $EventData variable will contain a hashtable of all the input fields and their values. | true |
| OnValidate | Endpoint | A script block that validates the form. Return the result of a call to New-UDFormValidationResult. | false |
| OnProcessing | ScriptBlock | A script block that is called when the form begins processing. The return value of this script block should be a component that displays a loading dialog. The script block will receive the current form data. | false |
| OnCancel | Endpoint | An endpoint that is called when this form is cancelled. When this parameter is defined a cancel button will appear. | false |



**New-UDFormValidationResult**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Valid | SwitchParameter | Whether the form status is considered valid. | false |
| ValidationError | String | An error to display if the form is not valid. | false |

