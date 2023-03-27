---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUFileAssociation

## SYNOPSIS
Creates a new file association within Windows to a script. Only supported by PSU Desktop.

## SYNTAX

```
New-PSUFileAssociation [-Script] <Script> [-Credential <Variable>] [-Environment <String>]
 [-Extension <String>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

## DESCRIPTION
Creates a new file association within Windows to a script. Only supported by PSU Desktop.

## EXAMPLES

### Example 1
```powershell
PS C:\> New-PSUFileAssociation -Script FileAssociation.ps1 -Extension .ps3
```

creates a file association to the *.ps3 file type and runs the FileAssocation.ps1 file when it's opened.

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

### -Extension
The file extension to use. 

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

### -Script
The script to run when the associated file is opened.

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
