---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# New-PSUScript

## SYNOPSIS

Creates a new script within PowerShell Universal. 

## SYNTAX

### ScriptBlock
```
New-PSUScript -ScriptBlock <ScriptBlock> [-ManualTime <Int32>] [-TimeOut <Double>] -Name <String>
 [-Description <String>] [-Parameter <ScriptParameter[]>] [-Tag <Tag[]>] [-Status <ScriptStatus>]
 [-Folder <Folder>] [-Environment <String>] [-Notes <String>] [-DisableManualInvocation] [-MaxHistory <Int32>]
 [-ConcurrentJobs <Int32>] [-Credential <Variable>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [<CommonParameters>]
```

### Path
```
New-PSUScript [-ManualTime <Int32>] [-TimeOut <Double>] -Name <String> [-Description <String>]
 [-Parameter <ScriptParameter[]>] [-Tag <Tag[]>] [-Status <ScriptStatus>] [-Folder <Folder>]
 [-Environment <String>] [-Notes <String>] [-DisableManualInvocation] -Path <String> [-MaxHistory <Int32>]
 [-ConcurrentJobs <Int32>] [-Credential <Variable>] [-ComputerName <String>] [-AppToken <String>]
 [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION

Creates a new script within PowerShell Universal. Scripts can be manually executed or scheduled inside PSU. Scripts created based on content will be written to the repository directory. Scripts created by path will be referenced by that path. 

Script configurations are stored in .universal/scripts.ps1

You can also use this cmdlet to create scripts through the REST API.

## EXAMPLES

### Example 1
```
New-PSUScript -Name 'Script1.ps1' -Path 'Script1.ps1'
```

Creates a script within PSU that references a relative path of Script1.ps1 in the repository folder. 

### Example 2
```
New-PSUScript -Name 'Script1.ps1' -ScriptBlock {
    "Hello, world!"
}
```

Creates a script within PSU based on the script block provided. This will create a Script1.ps1 file within the repository directory. 

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
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Description

The description of the script. 

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

### -DisableManualInvocation

Disables manual invocation of the script. The script can only be run on a schedule. 

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

### -Folder

The folder in which the script is stored. 

```yaml
Type: Folder
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ManualTime

The amount of time it would take to run this particular script manually.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MaxHistory

The maximum job history for this script. This defaults to 100.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name

The name of this script.

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

### -Notes

Notes to include with this script.

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

### -Parameter

Obsolete

```yaml
Type: ScriptParameter[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path

The path to the script. This can be a relative path to the repository directory or an absolute path. 

```yaml
Type: String
Parameter Sets: Path
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ScriptBlock

A script block to define for this script. 

```yaml
Type: ScriptBlock
Parameter Sets: ScriptBlock
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Status

Not used. 

```yaml
Type: ScriptStatus
Parameter Sets: (All)
Aliases:
Accepted values: Draft, Pending_Review, Published, Disabled

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Tag

Tags to assign to this script.

```yaml
Type: Tag[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ConcurrentJobs

The number of concurrent jobs that are allowed for this script. By default, there is no limit.

```yaml
Type: Int32
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Environment

The environment to run this script within. 

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

### -TimeOut

The number of minutes before jobs based on this script will time out. 

```yaml
Type: Double
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
The user credential variable to use when executing this script.

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

[Get-PSUScript](Get-PSUScript)
[Remove-PSUScript](Remove-PSUScript)
[Invoke-PSUScript](Invoke-PSUScript)
[Set-PSUScript](Set-PSUScript)
[Get-PSUEnvironment](Get-PSUEnvironment)