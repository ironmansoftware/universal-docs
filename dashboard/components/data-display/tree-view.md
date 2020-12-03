---
description: Tree view component for Universal Dashboard.
---

# Tree View

`New-UDTreeView` allows you to create a tree of items and, optionally, dynamically expand the list when clicked.

## Basic Tree View 

Create a basic tree view by using the `New-UDTreeNode` cmdlet. 

```text
New-UDTreeView -Node {
    New-UDTreeNode -Name 'Level 1' -Children {
        New-UDTreeNode -Name 'Level 2 - Item 1' 
        New-UDTreeNode -Name 'Level 2 - Item 2'
        New-UDTreeNode -Name 'Level 2 - Item 3' -Children {
            New-UDTreeNode -Name 'Level 3'
        }
    }
}
```

![Basic Tree View](../../../.gitbook/assets/image%20%28163%29.png)

## Dynamic Tree View

Dynamic tree views allow you to run PowerShell whenever a node is clicked. You can then return a list of nodes that should be rendered underneath the clicked node. You can also take other actions such as opening a modal or showing a toast. 

```text
New-UDTreeView -Node { New-UDTreeNode -Name root } -OnNodeClicked {
    New-UDTreeNode -name "$($EventData.Name)child"
}
```

![Dynamic Tree View](../../../.gitbook/assets/image%20%28161%29.png)



