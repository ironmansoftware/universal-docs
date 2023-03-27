---
external help file: Universal-help.xml
Module Name: Universal
online version:
schema: 2.0.0
---

# Update-PSUServer

## SYNOPSIS
Update the PowerShell Universal server.

## SYNTAX

### Version (Default)
```
Update-PSUServer [-Path <String>] [-Version <String>] [-IISWebsite <String>] [<CommonParameters>]
```

### Latest
```
Update-PSUServer [-Path <String>] [-LatestVersion] [-IISWebsite <String>] [<CommonParameters>]
```

## DESCRIPTION
Update the PowerShell Universal server.
This is a convenience function that will update the server for your platform.

## EXAMPLES

### EXAMPLE 1
```
Update-PSUServer
```

## PARAMETERS

### -Path
The path for the PowerShell Universal binaries.
If not specified, the path will attempt to be resolved.

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

### -Version
The version to upgrade to.

```yaml
Type: String
Parameter Sets: Version
Aliases:

Required: False
Position: Named
Default value: (Get-Module Universal).Version
Accept pipeline input: False
Accept wildcard characters: False
```

### -LatestVersion
Upgrade to the latest version.

```yaml
Type: SwitchParameter
Parameter Sets: Latest
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -IISWebsite
The IIS website to update.

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

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES

## RELATED LINKS
