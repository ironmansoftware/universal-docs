---
description: Date and time component for Universal Apps.
---

# Date and Time

The `New-UDDateTime` component is used for formatting dates and times within the client's browser. By using the client's browser, you can format the time based on the local time zone and locale settings for the user.

{% hint style="warning" %}
The output of `New-UDDateTime` cannot be used with components like `New-UDHtml`, `New-UDMarkdown` or `Show-UDToast`. The object returned by `New-UDDateTime` needs to run JavaScript within the browser and is not an actual DateTime object.
{% endhint %}

The date and time component uses DayJS. For a full list of custom formatting options, visit the [DayJS documentation](https://day.js.org/docs/en/display/format).

## Basic Formatting

By default, the date and time will be formatted using the `LLL` localized formatting template.

```powershell
New-UDDateTime -InputObject (Get-Date)
```

Resulting output: August 16, 2018 8:02 PM

## Custom Formatting

You can specify custom formatting strings using the [DayJS formatting template](https://day.js.org/docs/en/display/format).

```powershell
New-UDDateTime -InputObject (Get-Date) -Format 'DD/MM/YYYY'
```

Resulting output: 25/01/2019

## Locale

You can specify the locale to display the date and time in.

```powershell
New-UDDateTime -InputObject (Get-Date) -Locale 'es'
```

Resulting output: 13 de septiembre de 2022 7:30

## API

[**New-UDDateTime**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDDateTime.txt)
