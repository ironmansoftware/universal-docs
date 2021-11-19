---
description: Expansion Panel component for Universal Dashboard
---

# Expansion Panel

**Expansion panels contain creation flows and allow lightweight editing of an element.**

An expansion panel is a lightweight container that may either stand alone or be connected to a larger surface, such as a card.

## Simple Expansion Panel

![](<../../../../.gitbook/assets/image (78).png>)

```powershell
New-UDExpansionPanelGroup -Children {
    New-UDExpansionPanel -Title "Hello" -Children {}

    New-UDExpansionPanel -Title "Hello" -Id 'expContent' -Children {
        New-UDElement -Tag 'div' -Content { "Hello" }
    }
}
```

## API

* [New-UDExpansionPanel](../../../../cmdlets/New-UDExpansionPanel.txt)
* [New-UDExpansionPanelGroup](../../../../cmdlets/New-UDExpansionPanelGroup.txt)
