---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-UAFolder

## SYNOPSIS
Creates a new folder within UA.

## SYNTAX

### Name
```
New-UAFolder -Name <String> [-Parent <Folder>] [-ComputerName <String>] [-AppToken <String>]
 [<CommonParameters>]
```

### Path
```
New-UAFolder [-Path <String>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new folder within UA.
This will create a new folder within the internal git repository and additionally a configured remote.

## EXAMPLES

### Example 1
```
PS C:\> New-UAFolder -Name 'Scripts'
```

Creates a new Scripts folder in the root of the UA folder structure.

### Example 2
```
PS C:\> $Parent = Get-UAFolder -Name 'Scripts'
PS C:\> New-UAFolder -Name 'Private' -Parent $Parent
```

Creates a new Private folder in the Scripts folder of the UA folder structure.

## PARAMETERS

### -AppToken
An app token to access the UA API.

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
The HTTP address of the UA REST API server.

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

### -Name
The name of the folder to create.

```yaml
Type: String
Parameter Sets: Name
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Parent
The parent folder to create this folder underneath.

```yaml
Type: Folder
Parameter Sets: Name
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
{{ Fill Path Description }}

```yaml
Type: String
Parameter Sets: Path
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
