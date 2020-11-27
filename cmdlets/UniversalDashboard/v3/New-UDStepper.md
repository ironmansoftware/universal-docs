---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDStepper

## SYNOPSIS
Creates a new stepper component.

## SYNTAX

```
New-UDStepper [[-Id] <String>] [[-ActiveStep] <Int32>] [-Children] <ScriptBlock> [-NonLinear]
 [-AlternativeLabel] [-OnFinish] <Endpoint> [[-OnValidateStep] <Endpoint>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new stepper component.
Steppers can be used as multi-step forms or to display information in a stepped manner.

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

### -ActiveStep
Sets the active step.
This should be the index of the step.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: 0
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
The steps for this stepper.
Use New-UDStep to create new steps.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases: Steps

Required: True
Position: 3
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NonLinear
Allows the user to progress to steps out of order.

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

### -AlternativeLabel
Places the step label under the step number.

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

### -OnFinish
A script block that is executed when the stepper is finished.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: True
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnValidateStep
\[Parameter()\]
\[Endpoint\]$OnCompleteStep,

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 5
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
