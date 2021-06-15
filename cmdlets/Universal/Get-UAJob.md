---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-UAJob

## SYNOPSIS
Returns jobs run within UA.

## SYNTAX

### All (Default)
```
Get-UAJob [-Status <JobStatus>] [-OrderBy <String>] [-OrderDirection <OrderDirection>] [-ComputerName <String>]
 [-AppToken <String>] [-UseDefaultCredentials] [-IncludeTotalCount] [-Skip <UInt64>] [-First <UInt64>]
 [<CommonParameters>]
```

### Id
```
Get-UAJob [-Id] <Int64> [-Status <JobStatus>] [-OrderBy <String>] [-OrderDirection <OrderDirection>]
 [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-IncludeTotalCount] [-Skip <UInt64>]
 [-First <UInt64>] [<CommonParameters>]
```

### Identity
```
Get-UAJob [-Identity] <Identity> [-Status <JobStatus>] [-OrderBy <String>] [-OrderDirection <OrderDirection>]
 [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-IncludeTotalCount] [-Skip <UInt64>]
 [-First <UInt64>] [<CommonParameters>]
```

### Script
```
Get-UAJob [-Script] <Script> [-Status <JobStatus>] [-OrderBy <String>] [-OrderDirection <OrderDirection>]
 [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials] [-IncludeTotalCount] [-Skip <UInt64>]
 [-First <UInt64>] [<CommonParameters>]
```

## DESCRIPTION
Returns jobs run within UA.

## EXAMPLES

### Example 1
```
PS C:\> Get-UAJob
```

Returns all jobs run in UA.

### Example 2
```
PS C:\> Get-UAJob -Id 10
```

Returns job 10 from UA.

### Example 3
```
PS C:\> $Script = Get-UAScript -Id 4
PS C:\> Get-UAJob -Script $Script
```

Returns all jobs run for script with Id 4.

### Example 4
```
PS C:\> Get-UAJob -Id 10 -Tree
```

Returns job 10 and any jobs (parent\child jobs) associated with it.

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

### -First
Gets only the specified number of objects.
Enter the number of objects to get.

```yaml
Type: UInt64
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of the job to return.

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

### -Identity
Returns jobs run by this identity.

```yaml
Type: Identity
Parameter Sets: Identity
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -IncludeTotalCount
Reports the total number of objects in the data set (an integer) followed by the selected objects.
If the cmdlet cannot determine the total count, it displays "Unknown total count." The integer has an Accuracy property that indicates the reliability of the total count value.
The value of Accuracy ranges from 0.0 to 1.0 where 0.0 means that the cmdlet could not count the objects, 1.0 means that the count is exact, and a value between 0.0 and 1.0 indicates an increasingly reliable estimate.

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

### -OrderBy
Orders the output based on the property selected.

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Accepted values: Id, StartTime, EndTime

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OrderDirection
Orders ascending or descending.

```yaml
Type: OrderDirection
Parameter Sets: (All)
Aliases:
Accepted values: Descending, Ascending

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Script
Returns jobs based on this script.

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

### -Skip
Ignores the specified number of objects and then gets the remaining objects.
Enter the number of objects to skip.

```yaml
Type: UInt64
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Status
Filters output based on this status.

```yaml
Type: JobStatus
Parameter Sets: (All)
Aliases:
Accepted values: Queued, Running, Completed, Failed, WaitingOnFeedback, Canceled, Canceling, Historical, Active

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

### UniversalAutomation.Identity
### UniversalAutomation.Script
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
