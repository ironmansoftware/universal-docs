---
description: Autocomplete component for Universal Dashboard
---

# Autocomplete

The autocomplete is a normal text input enhanced by a panel of suggested options.

## Autocomplete with a static list of options

Creates a basic autocomplete with a static list of options

```powershell
New-UDAutocomplete -Options @('Test', 'Test2', 'Test3', 'Test4')
```

## Autocomplete with a dynamic list of options

When text is typed, it can be filtered with `OnLoadOptions`. `$Body` will contain the current text that is typed.&#x20;

This example filters the array with `Where-Object`.&#x20;

```powershell
New-UDAutocomplete -OnLoadOptions { 
    @('Test', 'Test2', 'Test3', 'Test4') | Where-Object { $_ -like "*$Body*" } | ConvertTo-Json
}
```

## Autocomplete with an OnChange script block

`$Body` contains the currently selected item.&#x20;

```powershell
New-UDAutocomplete -OnLoadOptions { 
    @('Test', 'Test2', 'Test3', 'Test4') | Where-Object { $_ -like "*$Body*" } | ConvertTo-Json
} -OnChange {
    Show-UDToast $Body 
}
```

## API

* [New-UDAutocomplete](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDAutocomplete.txt)
