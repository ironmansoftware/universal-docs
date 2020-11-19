---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version:
schema: 2.0.0
---

# Add-UDDashboard

## SYNOPSIS
{{ Fill in the Synopsis }}

## SYNTAX

### FilePath
```
Add-UDDashboard -FilePath <String> -BaseUrl <String> -Name <String> -Framework <DashboardFramework>
 [-Environment <String>] [-GrantAppToken] [-Authenticated] [-Role <String>] [-DisableAutoStart]
 [-Component <DashboardComponent[]>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

### Content
```
Add-UDDashboard -Content <ScriptBlock> -BaseUrl <String> -Name <String> -Framework <DashboardFramework>
 [-Environment <String>] [-GrantAppToken] [-Authenticated] [-Role <String>] [-DisableAutoStart]
 [-Component <DashboardComponent[]>] [-ComputerName <String>] [-AppToken <String>] [<CommonParameters>]
```

## DESCRIPTION
{{ Fill in the Description }}

## EXAMPLES

### Example 1
```
PS C:\> {{ Add example code here }}
```

{{ Add example description here }}

## PARAMETERS

### -AppToken
{{ Fill AppToken Description }}

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

### -Authenticated
{{ Fill Authenticated Description }}

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

### -BaseUrl
{{ Fill BaseUrl Description }}

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

### -ComputerName
{{ Fill ComputerName Description }}

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

### -FilePath
{{ Fill FilePath Description }}

```yaml
Type: String
Parameter Sets: FilePath
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Framework
{{ Fill Framework Description }}

```yaml
Type: DashboardFramework
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -GrantAppToken
{{ Fill GrantAppToken Description }}

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

### -Name
{{ Fill Name Description }}

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

### -Component
{{ Fill Component Description }}

```yaml
Type: DashboardComponent[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
{{ Fill Content Description }}

```yaml
Type: ScriptBlock
Parameter Sets: Content
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -DisableAutoStart
{{ Fill DisableAutoStart Description }}

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

### -Role
{{ Fill Role Description }}

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

### None
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
