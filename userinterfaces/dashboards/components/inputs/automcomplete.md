---
description: Autocomplete component for Universal Dashboard
---

# Autocomplete

The autocomplete is a normal text input enhanced by a panel of suggested options.

## Static List of Options

Creates a basic autocomplete with a static list of options

```powershell
New-UDAutocomplete -Options @('Test', 'Test2', 'Test3', 'Test4')
```

## Dynamic List of Options

When text is typed, it can be filtered with `OnLoadOptions`. `$Body` will contain the current text that is typed.&#x20;

This example filters the array with `Where-Object`.&#x20;

```powershell
New-UDAutocomplete -OnLoadOptions { 
    @('Test', 'Test2', 'Test3', 'Test4') | Where-Object { $_ -like "*$Body*" } | ConvertTo-Json
}
```

## OnChange

`$Body` contains the currently selected item. The OnChange event will fire when the user selects one or more items.

```powershell
New-UDAutocomplete -OnLoadOptions { 
    @('Test', 'Test2', 'Test3', 'Test4') | Where-Object { $_ -like "*$Body*" } | ConvertTo-Json
} -OnChange {
    Show-UDToast $Body 
}
```

## Icon&#x20;

![](<../../../../.gitbook/assets/image (383).png>)

You can place an icon before an autocomplete by using the `-Icon` parameter.

```powershell
New-UDAutocomplete -Options @("Test", "No", "Yes") -Icon (New-UDIcon -Icon 'Users') 
```

## OnEnter

OnEnter is triggered when the user presses the enter key within the autocomplete.

```powershell
New-UDAutocomplete -Options @("Test", "No", "Yes") -onEnter {
    Show-UDToast ((Get-UDElement -Id 'ac').value)
} -Id 'ac'
```

## Options

You can use `New-UDAutoCompleteOption` to specify name and values.&#x20;

```powershell
New-UDAutocomplete -Options @(
    New-UDAutoCompleteOption -Name 'Adam D' -Value '1'
    New-UDAutoCompleteOption -Name 'Sarah F' -Value '2'
    New-UDAutoCompleteOption -Name 'Tom S' -Value '3'
)
```

## API

* [New-UDAutocomplete](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDAutocomplete.txt)
