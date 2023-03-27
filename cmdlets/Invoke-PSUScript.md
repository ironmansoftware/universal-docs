---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Invoke-PSUScript

## SYNOPSIS
Invokes a script within UA.

## SYNTAX

### Script
```
Invoke-PSUScript [-Script] <Script> [-WaitForDebugger] [-Environment <String>] [-Notes <String>]
 [-Credential <Variable>] [-Wait] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### Id
```
Invoke-PSUScript [-Id] <Int64> [-WaitForDebugger] [-Environment <String>] [-Notes <String>]
 [-Credential <Variable>] [-Wait] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### Name
```
Invoke-PSUScript [-WaitForDebugger] [-Environment <String>] [-Notes <String>] [-Credential <Variable>]
 [-Name] <String> [-Wait] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-Integrated]
 [<CommonParameters>]
```

## DESCRIPTION
Invokes a script within UA.
Invoking a script starts a new job that you can then track the progress of.

## EXAMPLES

### Example 1
```
PS C:\> $Script = Get-PSUScript -Name 'Script1.ps1'
PS C:\> Invoke-PSUScript -Script $Script
```

Invokes 'Script1.ps1'

### Example 2
```
PS C:\> $Script = Get-PSUScript -Name 'Script1.ps1'
PS C:\> Invoke-PSUScript -Script $Script -Parameter1 123 -Parameter2 "Test"
```

Invokes 'Script1.ps1' with the parameters Parameter1 and Parameter2.
These parameters will be passed to the script.
Invoke-PSUScript supports any number of dynamic parameters.

### Example 3
```
PS C:\> $Script = Get-PSUScript -Name 'Script1.ps1'
PS C:\> $Password = Get-UAVariable -Name 'UserPassword'
PS C:\> $Credential = New-UDCredential -UserName 'adam' -Password $Password
PS C:\> Invoke-PSUScript -Script $Script -Credential $Credential
```

Invokes 'Script1.ps1' as the user 'adam'.
Passwords are retrieved from secret managers and cannot be passed in as strings.

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
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
The credential of the user to run the script as.
Use New-UACredential to create this credential.

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
The environment to use when invoke this script. You can see available environments by using Get-PSUEnvironment.

```yaml
Type: String
Parameter Sets: (All)
Aliases: PowerShellVersion

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of the script to invoke.

```yaml
Type: Int64
Parameter Sets: Id
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Integrated
Executes the command internally rather than using the Management API. Only works when running script from within PowerShell Universal. 

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

### -Name
The name of the script to invoke.

```yaml
Type: String
Parameter Sets: Name
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Notes
Notes to include with the job execution.

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
The script to invoke.
Use Get-PSUScript to retrieve existing scripts.

```yaml
Type: Script
Parameter Sets: Script
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
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

### -Wait
{{ Fill Wait Description }}

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

### -WaitForDebugger
Not used.

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

### UniversalAutomation.Script
### System.Int64
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS

[Get-PSUEnvironment](Get-PSUEnvironment.md)