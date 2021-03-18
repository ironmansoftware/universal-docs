---
description: Autocomplete component for Universal Dashboard
---

# Autocomplete

The autocomplete is a normal text input enhanced by a panel of suggested options.

## Autocomplete with a static list of options

```PowerShell
New-UDAutocomplete -Options @('Test', 'Test2', 'Test3', 'Test4') 
```

## Autocomplete with a dynamic list of options

```PowerShell
New-UDAutocomplete -OnLoadOptions { 
    @('Test', 'Test2', 'Test3', 'Test4') | Where-Object { $_ -match $Body } | ConvertTo-Json
}
```

## Autocomplete with an OnChange script block

```PowerShell
New-UDAutocomplete -OnLoadOptions { 
    @('Test', 'Test2', 'Test3', 'Test4') | Where-Object { $_ -match $Body } | ConvertTo-Json
} -OnChange {
    Show-UDToast $Body 
}
```

