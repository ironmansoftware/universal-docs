---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version:
schema: 2.0.0
---

# Connect-PSUServer

## SYNOPSIS
Connects to a PowerShell Universal server.

## SYNTAX

```
Connect-PSUServer -ComputerName <String> [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION
Connects to a PowerShell Universal server. When you connect using this cmdlet, you will no longer need to specify the -ComputerName and -AppToken parameters for each cmdlet that is accessing the PowerShell Universal Management API.

## EXAMPLES

### Example 1
```powershell
PS C:\> Connect-PSUServer -ComputerName http://localhost:5000 -AppToken 'appToken123'
```

Connects to the PSU server listening on port 5000 of localhost using the app token appToken123.

## PARAMETERS

### -AppToken
The AppToken that is used for calling the PowerShell Universal Management API. You can also call Connect-PSUServer before calling this cmdlet to set the AppToken for the entire session.

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
Specifies the computer name or URL that should be called when accessing the PowerShell Universal Management API. You can also use Connect-PSUServer before calling this cmdlet to set the computer name for the entire session. 

```yaml
Type: String
Parameter Sets: (All)
Aliases: Url

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseDefaultCredentials
Use default credentials when connecting to the management API

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

### None

## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
