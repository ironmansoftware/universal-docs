---
description: Date Picker component for Universal Dashboard
---

# Date Picker

Date pickers pickers provide a simple way to select a single value from a pre-determined set.

Date pickers can be used in [Forms](form.md) and [Steppers](../navigation/stepper.md).

![](../../../../.gitbook/assets/image%20%2873%29.png)

```text
New-UDDatePicker
```

## OnChange Event Handler

The OnChange event handler is called when the date changes. You can access the current date by using the `$Body` variable.

```text
New-UDDatePicker -OnChange {
    Show-UDToast -Message $body
}
```

## Variant

You can customize how the date picker is show. The default is the `inline` variant that displays the date picker popup inline with the input control. You can also use the `dialog` variant that pops the date picker up in the middle of the screen. Finally, the `static` variant displays the date picker without having to click anything.

```text
New-UDDatePicker -Variant static
```

## Locale

{% hint style="warning" %}
This feature is coming in PowerShell Universal 2.3.
{% endhint %}

To set the locate of the date picker, specify the `-Locale` parameter. 

```text
New-UDDatePicker -Locale fr
```

![](../../../../.gitbook/assets/image%20%28238%29.png)

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
| Locale | String | Specifies the locale for the date picker. Supports en, de, ru, and fr. Defaults to en. Available since 2.3. | false |

