---
description: Select component for Universal Dashboard
---

# Select

Select components are used for collecting user provided information from a list of options.

## Simple Select

Create a simple select with multiple options.

![](<../../../../.gitbook/assets/image (66).png>)

```powershell
New-UDSelect -Option {
    New-UDSelectOption -Name 'One' -Value 1
    New-UDSelectOption -Name 'Two' -Value 2
    New-UDSelectOption -Name 'Three' -Value 3
}
```

## Grouped Select

Create a select with groups of selections.

![](<../../../../.gitbook/assets/image (50).png>)

```powershell
New-UDSelect -Option {
    New-UDSelectGroup -Name 'Group One' -Option {
        New-UDSelectOption -Name 'One' -Value 1
        New-UDSelectOption -Name 'Two' -Value 2
        New-UDSelectOption -Name 'Three' -Value 3
    }
    New-UDSelectGroup -Name 'Group Two' -Option {
        New-UDSelectOption -Name 'Four' -Value 4
        New-UDSelectOption -Name 'Five' -Value 5
        New-UDSelectOption -Name 'Size' -Value 6
    }
}
```

## OnChange

Execute a PowerShell event handler when the value of the select is changed.

```powershell
New-UDSelect -Option {
    New-UDSelectOption -Name 'One' -Value 1
    New-UDSelectOption -Name 'Two' -Value 2
    New-UDSelectOption -Name 'Three' -Value 3
} -OnChange { Show-UDToast -Message $EventData }
```

## Get-UDElement

Retrieve the value of the select from another component.

```powershell
  New-UDSelect -Option {
      New-UDSelectOption -Name 'One' -Value 1
      New-UDSelectOption -Name 'Two' -Value 2
      New-UDSelectOption -Name 'Three' -Value 3
  } -Id 'select' -DefaultValue 2

  New-UDButton  -Text 'OnBoard' -OnClick {
    $Element = Get-UDElement -Id 'select'
    if ($Element.Value)
    {
      Show-UDToast -Message $Element.Value
    }
    else 
    {
      Show-UDToast -Message $Element.DefaultValue
    }
  }
```

## API

* [New-UDSelect](../../../../cmdlets/New-UDSelect.txt)
* [New-UDSelectOption](../../../../cmdlets/New-UDSelectOption.txt)
* [New-UDSelectGroup](../../../../cmdlets/New-UDSelectGroup.txt)

****

###
