---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTreeNode

## SYNOPSIS
Creates a tree node.

## SYNTAX

```
New-UDTreeNode [-Name] <String> [-Id <String>] [-Children <ScriptBlock>] [<CommonParameters>]
```

## DESCRIPTION
Creates a tree node.
This cmdlet should be used with New-UDTreeView.

## EXAMPLES

### EXAMPLE 1
```
See New-UDTreeView for examples.
```

## PARAMETERS

### -Name
The name of the node.
This is displayed within the UI.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Id
The ID of the node.
This is passed to the $EventData property when the OnNodeClicked script block is set.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: [Guid]::NewGuid()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Children
The children of this node.
This should be a collection of New-UDTreeNodes.

```yaml
Type: ScriptBlock
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
