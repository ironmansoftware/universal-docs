---
description: Expansion Panel component for Universal Dashboard
---

# Expansion Panel

**Expansion panels contain creation flows and allow lightweight editing of an element.**

An expansion panel is a lightweight container that may either stand alone or be connected to a larger surface, such as a card.

## Simple Expansion Panel

![](../../../.gitbook/assets/image%20%2878%29.png)

```PowerShell
New-UDExpansionPanelGroup -Children {
    New-UDExpansionPanel -Title "Hello" -Children {}

    New-UDExpansionPanel -Title "Hello" -Id 'expContent' -Children {
        New-UDElement -Tag 'div' -Content { "Hello" }
    }
}
```



**New-UDExpansionPanel**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Title | String | The title show within the header of the expansion panel. | false |
| Icon | FontAwesomeIcons | An icon to show within the header of the expansion panel. | false |
| Children | ScriptBlock | Children components to put within the expansion panel. | false |
| Active | SwitchParameter | Whether the expansion panel is currently active \(open\). | false |

