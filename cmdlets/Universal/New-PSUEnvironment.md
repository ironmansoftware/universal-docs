---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUEnvironment

## SYNOPSIS

Creates a new PowerShell Universal environment. 

## SYNTAX

```
New-PSUEnvironment -Name <String> -Path <String> [-Arguments <String>] [-Modules <String[]>]
 [-Variables <String[]>] [-PSModulePath <String[]>] [-PersistentRunspace] [-ComputerName <String>]
 [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION

Environments define PowerShell execution environments within PowerShell Universal. You can use them when executing APIs, Scripts, Dashboards and the security processes for authentication and authorization. 

Environments are stored within the ./universal/environments.ps1 file. 

You can also use this cmdlet to create environments through the REST API.

## EXAMPLES

### Example 1
```powershell
PS C:\> New-PSUEnvironment -Name '7.1' -Path 'pwsh.exe' 
```

Creates a new environment called 7.1 that uses the pwsh.exe for running APIs, scripts or dashboards. 

### Example 2
```powershell
PS C:\> New-PSUEnvironment -Name '7.1' -Path 'pwsh.exe' -ArgumentList "-ExecutionPolicy Bypass"
```

Creates a new environment called 7.1 that uses the pwsh.exe executable and sets the execution policy to ByPass. 

### Example 3
```powershell
PS C:\> New-PSUEnvironment -Name '7.1' -Path 'pwsh.exe' -ArgumentList "-ExecutionPolicy Bypass" -Variables @("*")
```

Creates a new environment that uses all the variables defined with New-PSUVariable. 


### Example 4
```powershell
PS C:\> New-PSUEnvironment -Name '7.1' -Path 'pwsh.exe' -ArgumentList "-ExecutionPolicy Bypass" -Modules @("ActiveDirectory")
```

Creates a new environment that automatically loads the ActiveDirectory module.

### Example 5
```powershell
PS C:\> New-PSUEnvironment -Name '7.1' -Path 'pwsh.exe' -ArgumentList "-ExecutionPolicy Bypass" -PersistentRunspace
```

Creates a new environment that uses persistent runspaces. Persistent runspaces are used for APIs and do not reset between each execution.

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

### -Arguments
Arguments to pass to the PowerShell process when starting the environment.

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
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Modules
Modules to automatically load when creating new runspaces in the environment.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
The name of the environment. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PSModulePath
Additional paths to add to the PSModulePath for the environment. 

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
The path to the PowerShell executable. 

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PersistentRunspace
Whether to enable persistent runspaces. This is only used for APIs. 

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

### -Variables
Variables to import into the runspace. These are variables defined by New-PSUVariable. 

```yaml
Type: String[]
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

[New-PSUVariable](New-UAVariable.md)