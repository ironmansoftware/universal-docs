---
description: This sample uses UDStyle to change the font size of the tree view control.
---

# Tree View Font Size

In this example, we use UDStyle to change the font size of the tree item labels. You can view a full list of CSS classes for the [tree view here](https://mui.com/material-ui/api/tree-item/#css).

<figure><img src="../../.gitbook/assets/image (573).png" alt=""><figcaption></figcaption></figure>

```powershell
New-UDStyle -Content {
    New-UDTreeView -Id "Tree1" -Expanded -Node {
        New-UDTreeNode -Name "Pre-Project" -Children {
            New-UDTreeNode -Name "Recorded Walkthrough of Process"
        }
    
        New-UDTreeNode -Name "Project Kick-Off" -Children {
            New-UDTreeNode -Name "Create project kickoff slide deck"
    
            New-UDTreeNode -Name "Verify Development Environment" -Children {
                New-UDTreeNode -Name "Verify client VPN connectivity"
                New-UDTreeNode -Name "Verify client internal network access"
                New-UDTreeNode -Name "Verify development Windows Device"
            }
        }
    } -Style @{
        "width" = 800
    }
} -Style ".MuiTreeItem-label { font-size: 25px }"
```
