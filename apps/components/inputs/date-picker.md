---
description: Date Picker component for Universal Apps
---

# Date Picker

Date pickers pickers provide a simple way to select a single value from a pre-determined set.

Date pickers can be used in [Forms](form.md) and [Steppers](../navigation/stepper.md).

![](<../../../.gitbook/assets/image (81).png>)

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

You can customize how the date picker is shown. The default is the `inline` variant that displays the date picker popup in line with the input control. The `static` variant displays the date picker without having to click anything.

```powershell
New-UDDatePicker -Variant static
```

## Locale

To set the locate of the date picker, specify the `-Locale` parameter.

```powershell
New-UDDatePicker -Locale fr
```

![](<../../../.gitbook/assets/image (50).png>)

## Minimum and Maximum

By default, the user can select any date. To specify minimum and maximum dates, using the `-Minimum` and `-Maximum` parameters.

```powershell
New-UDDatePicker -Minimum ((Get-Date).AddDays(-15)) -Maximum ((Get-Date).AddDays(15))
```

## Views

You can limit which portions of the date picker are included by using the `-Views` parameter. For example, if you wanted to remove the year selector and limit to the current year, you could do the following.&#x20;

```powershell
$Year = (Get-Date).Year
$MinDate = [DateTime]::new($year, 1, 1)
$MaxDate = [DateTime]::new($year, 12, 31)
New-UDDatePicker -Views "day" -MinimumDate $MinDate -MaximumDate $MaxDate
```

## API

* [New-UDDatePicker](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDDatePicker.txt)
