---
description: Date Picker component for Universal Dashboard
---

# Date Picker

Date pickers pickers provide a simple way to select a single value from a pre-determined set.

Date pickers can be used in [Forms](form.md) and [Steppers](../navigation/stepper.md).

![](<../../../../.gitbook/assets/image (73).png>)

```powershell
New-UDDatePicker
```

## OnChange Event Handler

The OnChange event handler is called when the date changes. You can access the current date by using the `$Body` variable.

```powershell
New-UDDatePicker -OnChange {
    Show-UDToast -Message $body
}
```

## Variant

You can customize how the date picker is show. The default is the `inline` variant that displays the date picker popup inline with the input control. You can also use the `dialog` variant that pops the date picker up in the middle of the screen. Finally, the `static` variant displays the date picker without having to click anything.

```powershell
New-UDDatePicker -Variant static
```

## Locale

To set the locate of the date picker, specify the `-Locale` parameter.&#x20;

```powershell
New-UDDatePicker -Locale fr
```

![](<../../../../.gitbook/assets/image (243).png>)

## API

* [New-UDDatePicker](../../../../cmdlets/New-UDDatePicker.txt)

****
