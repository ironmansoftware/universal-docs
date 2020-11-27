---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDForm

## SYNOPSIS
Creates a new form.

## SYNTAX

```
New-UDForm [[-Id] <String>] [-Children] <ScriptBlock> [-OnSubmit] <Endpoint> [[-OnValidate] <Endpoint>]
 [[-OnProcessing] <ScriptBlock>] [[-OnCancel] <Endpoint>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new form.
Forms can contain any set of input controls.
Each of the controls will report its value back up to the form when the submit button is clicked.

## EXAMPLES

### EXAMPLE 1
```
Creates a form that contains many input controls and displays the $eventdata hashtable as a toast.
```

New-UDForm -Id 'defaultForm' -Content {
    New-UDTextbox -Id 'txtNameDefault' -Value 'Name'
    New-UDTextbox -Id 'txtLastNameDefault' -Value 'LastName'
    New-UDCheckbox -Id 'chkYesDefault' -Label YesOrNo -Checked $true

    New-UDSelect -Label '1-3' -Id 'selectDefault' -Option {
        New-UDSelectOption -Name "OneDefault" -Value 1
        New-UDSelectOption -Name "TwoDefault" -Value 2
        New-UDSelectOption -Name "ThreeDefault" -Value 3
    } -DefaultValue '1'

    New-UDSwitch -Id 'switchYesDefault' -Checked $true

    New-UDDatePicker -Id 'dateDateDefault' -Value '1-2-2020'

    New-UDTimePicker -Id 'timePickerDefault' -Value '10:30 AM'

    New-UDRadioGroup -Label 'group' -Id 'simpleRadioDefault' -Children {
        New-UDRadio -Value 'Adam' -Label 'Adam'  -Id 'adamDefault'
        New-UDRadio -Value 'Alon' -Label 'Alon' -Id 'alonDefault'
        New-UDRadio -Value 'Lee' -Label 'Lee' -Id 'leeDefault'
    } -Value 'Adam'
} -OnSubmit {
    Show-UDToast -Message $Body
}

## PARAMETERS

### -Id
The ID of the component.
It defaults to a random GUID.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: [Guid]::NewGuid().ToString()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
Controls that make up this form.
This can be any combination of controls.
Input controls will report their state to the form.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: Content

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnSubmit
A script block that is execute when the form is submitted.
You can return controls from this script block and the form will be replaced by the script block.
The $EventData variable will contain a hashtable of all the input fields and their values.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: True
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnValidate
A script block that validates the form.
Return the result of a call to New-UDFormValidationResult.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnProcessing
A script block that is called when the form begins processing.
The return value of this script block should be a component that displays a loading dialog.
The script block will receive the current form data.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnCancel
{{ Fill OnCancel Description }}

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 6
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
