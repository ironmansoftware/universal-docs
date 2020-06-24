---
description: Switch component for Universal Dashboard
---

# Switch

Switches toggle the state of a single setting on or off.

Switches are the preferred way to adjust settings on mobile. The option that the switch controls, as well as the state it’s in, should be made clear from the corresponding inline label.

## Switch

```text
New-UDSwitch -Checked $true 
New-UDSwitch -Checked $true -Disabled
```

## OnChange Event

```text
New-UDSwitch -OnChange { Show-UDToast -Message $Body }
```

