---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Set-UAScript

## SYNOPSIS
Sets properties of a script.

## SYNTAX

### Id
```
Set-UAScript [-Id] <Int64> [-Name <String>] [-Description <String>] [-ManualTime <Double>] [-TimeOut <Double>]
 [-Status <String>] [-Content <String>] [-Notes <String>] [-Environment <String>]
 [-DisableManualInvocation <Boolean>] [-ScriptErrorAction <ActionPreference>] [-MaxHistory <Int32>]
 [-Tag <Tag[]>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

### Script
```
Set-UAScript [-Script] <Script> [-Name <String>] [-Description <String>] [-ManualTime <Double>]
 [-TimeOut <Double>] [-Status <String>] [-Content <String>] [-Notes <String>] [-Environment <String>]
 [-DisableManualInvocation <Boolean>] [-ScriptErrorAction <ActionPreference>] [-MaxHistory <Int32>]
 [-Tag <Tag[]>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

### ScriptBlock
```
Set-UAScript [-Name <String>] [-Description <String>] [-ManualTime <Double>] [-TimeOut <Double>]
 [-Status <String>] [-Content <String>] [-ScriptBlock <ScriptBlock>] [-Notes <String>] [-Environment <String>]
 [-DisableManualInvocation <Boolean>] [-ScriptErrorAction <ActionPreference>] [-MaxHistory <Int32>]
 [-Tag <Tag[]>] [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [<CommonParameters>]
```

## DESCRIPTION
Sets properties of a script.
Properties will be stored in both the database and the git repo.

## EXAMPLES

### Example 1
```
PS C:\> $Script = Get-UAScript -Name 'Script1.ps1'
PS C:\> Set-UAScript -Script $Script -Description 'My favorite script' -ManualTime 123
```

Sets the description and manual time of Script1.ps1.

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

### -Content
The content of the script.

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
Prevents this script from running manual.
It can only run by schedule.

```yaml
Type: Boolean
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of the script to set.

```yaml
Type: Int64
Parameter Sets: Id
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ManualTime
The manual execution time of this script.

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

### -MaxHistory
{{ Fill MaxHistory Description }}

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

Required: False
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

### -Script
The script to set properties on.
Use Get-UAScript to retrieve a Script object.

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

### -ScriptBlock
The script block used to set the content of the script.

```yaml
Type: ScriptBlock
Parameter Sets: ScriptBlock
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ScriptErrorAction
{{ Fill ScriptErrorAction Description }}

```yaml
Type: ActionPreference
Parameter Sets: (All)
Aliases:
Accepted values: SilentlyContinue, Stop, Continue, Inquire, Ignore, Suspend

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Status
The status of the script.
This is not currently used.

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Accepted values: Draft, Pending Review, Pending, Review, Published, Disabled

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Environment
{{ Fill Environment Description }}

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
{{ Fill TimeOut Description }}

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

### -Tag
Sets the tags for a script.

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

### UniversalAutomation.Script
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
