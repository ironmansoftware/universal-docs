---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDStep

## SYNOPSIS
Creates a new step for a stepper.

## SYNTAX

```
New-UDStep [[-Id] <String>] [-OnLoad] <Endpoint> [[-Label] <String>] [-Optional] [<CommonParameters>]
```

## DESCRIPTION
Creates a new step for a stepper.
Add to the Children (alias Steps) parameter for New-UDStepper.

## EXAMPLES

### EXAMPLE 1
```
Creates a stepper that reports the stepper context with each step.
```

New-UDStepper -Id 'stepper' -Steps {
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
    New-UDTypography -Text 'Nice!
You did it!' -Variant h3
    New-UDElement -Tag 'div' -Id 'result' -Content {$Body}
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
Default value: ([Guid]::NewGuid())
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnLoad
The script block that is executed when the step is loaded.
The script block will receive the $Body parameter which contains JSON for the current state of the stepper.
If you are using form controls, their data will be availalble in the $Body.Context property.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases: Content

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Label
A label for this step.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Optional
Whether this step is optional.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
