---
description: Time picker component for Universal Dashboard
---

# Time Picker

Time pickers pickers provide a simple way to select a single value from a pre-determined set.

## Time Picker

![](<../../../../.gitbook/assets/image (55).png>)

```
New-UDTimePicker
```

## Locale

Specify the locale of the time picker.&#x20;

```
New-UDTimePicker -Locale fr
```

## 24-Hour Time

You can use the `-DisableAmPm` parameter to use 24-hour time.&#x20;

```powershell
New-UDTimePicker -DisableAmPm
```

## API

[New-UDTimePicker](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDTimePicker.txt)
