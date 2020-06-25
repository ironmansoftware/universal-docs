---
description: Date Picker component for Universal Dashboard
---

# Date Picker

Date pickers pickers provide a simple way to select a single value from a pre-determined set.

![](../../../.gitbook/assets/image%20%2864%29.png)

```text
New-UDDatePicker 
```



**New-UDDatePicker**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Label | String | The label to show next to the date picker. | false |
| Variant | String | The theme variant to apply to the date picker. | false |
| DisableToolbar | SwitchParameter | Disables the date picker toolbar. | false |
| OnChange | Endpoint | A script block to call with the selected date. The $EventData variable will be the date selected. | false |
| Format | String | The format of the date when it is selected. | false |
| Value | DateTime | The current value of the date picker. | false |

