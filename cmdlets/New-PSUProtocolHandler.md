---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUProtocolHandler

## SYNOPSIS
A custom protocol handler that runs a script. Only supported in PSU Desktop.

## SYNTAX

```
New-PSUProtocolHandler [-Script] <Script> [-Credential <Variable>] [-Environment <String>] [-Protocol <String>]
 [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
A custom protocol handler that runs a script. Only supported in PSU Desktop.

## EXAMPLES

### Example 1
```powershell
PS C:\> New-PSUProtocolHandler -Script ProtocolHandler.ps1 -Protocol psu
```

Creates a psu protocol handler. When a protocol link like psu://test is opened, for example from a web browser, the ProtocolHandler.ps1 script will be executed.

## PARAMETERS

### -AppToken
Not used

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ComputerName
Not used

```yaml
Type: String
Parameter Sets: (All)
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
The credential to use when running the script. 

```yaml
Type: Variable
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Environment
The environment to use when running the script. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Integrated
Not used

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Protocol
The protocol name. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Script
The script to run whene executing the protocol. 

```yaml
Type: Script
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -UseDefaultCredentials
Not used

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### PowerShellUniversal.Script

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
