---
description: Launch scripts when certain events happen in Windows.
---

# System Events

![System Events in the Admin Console](<../.gitbook/assets/image (314).png>)

System events subscribe to WMI events within Windows and run scripts. You can then take action by running scripts.&#x20;

## Defining a System Event

To define a system event, you can use the `New-PSUSystemEvent` cmdlet within the `systemEvents.ps1` file. The following example triggers the `systemEvent.ps1` script when a `pwsh.exe` process is started.

```powershell
New-PSUSystemEvent -Script "systemEvent.ps1" -Environment "Default" -Credential "Default" -Type "Create" -Condition "TargetInstance isa `"Win32_Process`" and TargetInstance.Name = `"pwsh.exe`"" -Name "PowerShell Started"
```

## Accessing Event Data

When a script is executed, you will receive a `$TargetInstance` parameter. This contains the WMI object that caused the event to trigger.&#x20;

```powershell
param($TargetInstance)

New-BurntToastNotification -Text "PowerShell Started! $TargetInstance"
```
