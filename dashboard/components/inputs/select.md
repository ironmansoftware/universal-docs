---
description: Select component for Universal Dashboard
---

# Select

Select components are used for collecting user provided information from a list of options.

## Simple Select

![](../../../.gitbook/assets/image%20%2859%29.png)

```text
New-UDSelect -Option {
    New-UDSelectOption -Name 'One' -Value 1
    New-UDSelectOption -Name 'Two' -Value 2
    New-UDSelectOption -Name 'Three' -Value 3
}
```

## Grouped Select

![](../../../.gitbook/assets/image%20%2847%29.png)

```text
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

```text
New-UDSelect -Option {
    New-UDSelectOption -Name 'One' -Value 1
    New-UDSelectOption -Name 'Two' -Value 2
    New-UDSelectOption -Name 'Three' -Value 3
} -OnChange { Show-UDToast -Message $Body }
```



**New-UDSelect**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Option | ScriptBlock | Options to include in this select. This can be either New-UDSelectOption or New-UDSelectGroup. | false |
| Label | String | The label to show with the select. | false |
| OnChange | Endpoint | A script block that is executed when the script changes. $EventData will be an array of the selected values. | false |
| DefaultValue | String | The default selected value. | false |
| Disabled | SwitchParameter | Whether this select is disabled. | false |
| Multiple | SwitchParameter | Whether you can select multiple values. | false |

