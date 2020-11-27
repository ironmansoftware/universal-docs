---
external help file: UniversalDashboard.MaterialUI-help.xml
Module Name: UniversalDashboard
online version:
schema: 2.0.0
---

# New-UDTreeView

## SYNOPSIS
Creates a new tree view.

## SYNTAX

```
New-UDTreeView [[-Id] <String>] [-Node] <ScriptBlock> [[-OnNodeClicked] <Endpoint>] [<CommonParameters>]
```

## DESCRIPTION
Creates a new tree view.

## EXAMPLES

### EXAMPLE 1
```
Creates a basic tree view.
```

New-UDTreeView -Node {
    New-UDTreeNode -Id 'Root' -Name 'Root' -Children {
        New-UDTreeNode -Id 'Level1' -Name 'Level 1' -Children {
            New-UDTreeNode -Id 'Level2' -Name 'Level 2'
        }
        New-UDTreeNode -Name 'Level 1' -Children {
            New-UDTreeNode -Name 'Level 2'
        }
        New-UDTreeNode -Name 'Level 1' -Children {
            New-UDTreeNode -Name 'Level 2'
        }   
    }
    New-UDTreeNode -Id 'Root2' -Name 'Root 2'
}

## PARAMETERS

### -Id
The ID of the component.
It defaults to a random GUID.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: [Guid]::NewGuid()
Accept pipeline input: False
Accept wildcard characters: False
```

### -Node
A collection of root nodes to show within the tree view.

```yaml
Type: ScriptBlock
Parameter Sets: (All)
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OnNodeClicked
A script block that is called when a node is clicked.
$EventData will contain the node that was clicked.

```yaml
Type: Endpoint
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
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
