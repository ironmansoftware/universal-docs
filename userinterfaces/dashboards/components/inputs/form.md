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

## Schema Forms

Instead of defining all the layout and logic for forms using cmdlets, you can also define a form based on a hashtable of schema. This version of forms is based on [react-jsonschema-form](https://react-jsonschema-form.readthedocs.io/en/latest/).

### Fields

You define fields that accept string, number, integer, enum and boolean types. This changes the type of input shown.&#x20;

```powershell
New-UDForm -Schema @{
   title = "Test Form"
   type = "object"
   properties = @{
       name = @{
           type = "string"
       }
       age = @{
           type = "number"
       }
   }
} -OnSubmit {
   # $EventData.name
   # $EventData.age
}
```

### Required Properties

You can use the `required` property to set a list of required properties.&#x20;

```powershell
New-UDForm -Schema @{
   title = "Test Form"
   type = "object"
   properties = @{
       name = @{
           type = "string"
       }
       age = @{
           type = "number"
       }
   }
   required = @('name')
} -OnSubmit {
   # $EventData.name
   # $EventData.age
}
```

{% hint style="warning" %}
Note that the properties need to be lower case! For example, you need to ensure the keys in your properties hashtable are lower case and the list of required properties are also lower case.&#x20;
{% endhint %}

```powershell
New-UDForm -Schema @{
	title = "Test"
	type = "object"
	properties = @{
	  hostname = @{
		  title = "Hostname"
		  type = "string"
	  }
	  ipaddress= @{
		  title = "IP Address"
		  type = "string"
		  format = "ipv4"
	  }
	  description = @{
		  title = "Server Description"
		  type = "string"
	  }
	  servertype = @{
		  title = "Server Type"
		  type = "string"                            
		  enum = "App","DB"
	  }
	  environment = @{
		  title = "Environment"
		  type = "string"
		  enum = "Prod", "Dev" , "QA"
	  }
	}
	required = @('hostname','ipaddress','description','servertype','environment')                    
	} -OnSubmit {
	Show-UDModal -Content {                        
	  New-UDTypography -Text $EventData.formData
	} -Footer {
	  New-UDButton -Text "Close" -OnClick {Hide-UDModal}
	} -Persistent
}
```

### Arrays

You can create forms that accept 0 to many objects. The user will be able to add and remove objects to the form.&#x20;

```powershell
New-UDForm -Schema @{
   title = "Test Form"
   type = "array"
   items = @{
      type = "object" 
       properties = @{
           name = @{
               type = "string"
           }
           age = @{
               type = "number"
           }
       }
   }
} -OnSubmit {
   # $EventData[0].name
   # $EventData[0].age
}
```

## Script Forms

You can automatically generate forms based on scripts in your PowerShell Universal environment. Script forms will generate input components based on the `param` block. Script forms automatically support progress and feedback.&#x20;

Script forms also support displaying the output as text or a table.&#x20;

```powershell
New-UDForm -Script "Script.ps1" -OutputType 'text'
```

## API

* [New-UDForm](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDForm.txt)
* [New-UDFormValidationResult](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDValidationResult.txt)
