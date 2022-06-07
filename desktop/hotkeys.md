---
description: About PowerShell Universal desktop hotkeys.
---

# Hotkeys

PowerShell Universal Desktop supports global hotkeys that can be used to invoke scripts with key chords.&#x20;

![Hotkeys Page in the Admin Console](<../.gitbook/assets/image (348) (1).png>)

## Define a Hotkey

To define a hotkey, you will need to edit the `hotkeys.ps1` file in the `.universal` folder or through the Settings \ Configurations page within the Admin Console.&#x20;

Hotkeys are defined using the `New-PSUHotkey` cmdlet. For example, the following will invoke `MyScript.ps1` when `Ctrl+I` is pressed anywhere within Windows.&#x20;

```powershell
New-PSUHotkey -Key I -ModifierKey Ctrl -Script 'MyScript.ps1'
```

## Environments&#x20;

You can define which environment the hotkey runs within by using the `-Environment` parameter.&#x20;

```powershell
New-PSUHotkey -Key I -ModifierKey Ctrl -Script 'MyScript.ps1' -Environment 'pwsh'
```

## Parameters&#x20;

You can define parameters passed to the script by using the dynamic parameters provided by `New-PSUHotKey`.&#x20;

For example, if a script accepts a `-Parameter1` parameter, you can define that on `New-PSUHotKey.`

```powershell
param($Parameter1)
```

Within the hotkey, just use `-Parameter1`.&#x20;

```powershell
New-PSUHotkey -Key I -ModifierKey Ctrl -Script 'MyScript.ps1' -Parameter1 'Test'
```
