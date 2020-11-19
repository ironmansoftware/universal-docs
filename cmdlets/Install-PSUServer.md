---
external help file: Universal-help.xml
Module Name: Universal
online version:
schema: 2.0.0
---

# Install-PSUServer

## SYNOPSIS

Downloads and installed the PowerShell Universal server binaries. 

## SYNTAX

### Version (Default)
```
Install-PSUServer [[-Path] <String>] [-AddToPath] [-Version <String>] [<CommonParameters>]
```

### Latest
```
Install-PSUServer [[-Path] <String>] [-AddToPath] [-LatestVersion] [<CommonParameters>]
```

## DESCRIPTION

Downloads and installed the PowerShell Universal server binaries. This cmdlet will download the proper binaries for the platform it is being run on. It can also add the binaries to the machine's PATH variable. 

## EXAMPLES

### Example 1
```
PS C:\> Install-PSUServer
```

Installs the PowerShell Universal version based on the module installed. If the module version is 1.5.0, then the 1.5.0 version is downloaded and installed. This installs to the default location of $Env:ProgramData\PowerShellUniversal. 

### Example 2
```
PS C:\> Install-PSUServer -AddToPath -LatestVersion
```

Installs the latest version of PowerShell Universal into the default location and sets the path in the PATH variable. 

### Example 3
```
PS C:\> Install-PSUServer -Path .\PSU
```

Installs the current version to the .\PSU folder. 

## PARAMETERS

### -Path

The path to where the PowerShell Universal binaries should be stored. This defaults to $Env:ProgramData\PowerShellUniversal

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -AddToPath

Adds the the path specified by -Path to the $env:PATH variable. 

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

### -LatestVersion

Downloads and installs the latest version of PowerShell Universal. 

```yaml
Type: SwitchParameter
Parameter Sets: Latest
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Version

The version to download. This defaults to the version of the PowerShell Universal module you are using. 

```yaml
Type: String
Parameter Sets: Version
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

[Start-PSUServer](Start-PSUServer)