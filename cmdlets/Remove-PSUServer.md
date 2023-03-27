---
external help file: Universal-help.xml
Module Name: Universal
online version:
schema: 2.0.0
---

# Remove-PSUServer

## SYNOPSIS
Removes the PowerShell Universal server.

## SYNTAX

```
Remove-PSUServer [[-Path] <String>] [[-IISWebsite] <String>] [<CommonParameters>]
```

## DESCRIPTION
Removes the PowerShell Universal server.
This is a convenience function that will remove the server for your platform.

## EXAMPLES

### EXAMPLE 1
```
Remove-PSUServer
```

## PARAMETERS

### -Path
The path to the PowerShell Universal binaries.
If not specified, the path will attempt to be resolved.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -IISWebsite
The IIS website to uninstall.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
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
