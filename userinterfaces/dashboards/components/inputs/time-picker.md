---
description: Time picker component for Universal Dashboard
---

# Time Picker

Time pickers pickers provide a simple way to select a single value from a pre-determined set.

## Time Picker

![](../../../../.gitbook/assets/image%20%2881%29.png)

```text
New-UDTimePicker
```

## Locale

Specify the locale of the time picker. 

```text
New-UDTimePicker -Locale fr
```

**New-UDTimePicker**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Label | String | The label to show with the time picker. | false |
| OnChange | Endpoint | A script block to call when the time is changed. The $EventData variable contains the currently selected time. | false |
| Value | String | The current value of the time picker. | false |
| Locale | String | The locale to use for the time picker. Supports en, de, ru, and fr. Defaults to en. Available since 2.3. | false |

