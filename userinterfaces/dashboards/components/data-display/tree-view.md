---
description: Tree view component for Universal Dashboard.
---

# Tree View

`New-UDTreeView` allows you to create a tree of items and, optionally, dynamically expand the list when clicked.

## Basic Tree View

Create a basic tree view by using the `New-UDTreeNode` cmdlet.

```powershell
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

![Basic Tree View](<../../../../.gitbook/assets/image (163).png>)

## Dynamic Tree View

Dynamic tree views allow you to run PowerShell whenever a node is clicked. You can then return a list of nodes that should be rendered underneath the clicked node. You can also take other actions such as opening a modal or showing a toast.

```powershell
New-UDDashboard -Title 'File System' -Content {
    Get-PSDrive -PSProvider 'FileSystem' | ForEach-Object {
        New-UDTreeView -Node { New-UDTreeNode -Name $_.Name -Id "$($_.Name):\" } -OnNodeClicked {
            Get-ChildItem $EventData.Id | ForEach-Object {
                New-UDTreeNode -Name $_.Name -Id $_.FullName -Leaf:$(-not $_.PSIsContainer)
            }
        }
    }
}
```

<figure><img src="../../../../.gitbook/assets/image (1) (4).png" alt=""><figcaption></figcaption></figure>

## API

* [New-UDTreeView](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDTreeView.txt)
* [New-UDTreeNode](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDTreeNode.txt)
