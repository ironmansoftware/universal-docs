---
description: Radio component for Universal Dashboard
---

# Radio

Radio buttons allow the user to select one option from a set.

Use radio buttons when the user needs to see all available options. If available options can be collapsed, consider using a dropdown menu because it uses less space.

Radio buttons should have the most commonly used option selected by default.

## Simple Radio

![](../../../.gitbook/assets/image%20%2852%29.png)

```text
New-UDRadioGroup -Label "Day" -Content {
    New-UDRadio -Label Monday -Value 'monday'
    New-UDRadio -Label Tuesday -Value 'tuesday'
    New-UDRadio -Label Wednesday -Value 'wednesday'
    New-UDRadio -Label Thursday -Value 'thursday'
    New-UDRadio -Label Friday  -Value 'friday'
    New-UDRadio -Label Saturday -Value 'saturday'
    New-UDRadio -Label Sunday -Value 'sunday'
}
```

## OnChange

```text
New-UDRadioGroup -Label "Day" -Content {
    New-UDRadio -Label Monday -Value 'monday'
    New-UDRadio -Label Tuesday -Value 'tuesday'
    New-UDRadio -Label Wednesday -Value 'wednesday'
    New-UDRadio -Label Thursday -Value 'thursday'
    New-UDRadio -Label Friday  -Value 'friday'
    New-UDRadio -Label Saturday -Value 'saturday'
    New-UDRadio -Label Sunday -Value 'sunday'
} -OnChange { Show-UDToast -Message $Body }
    }
```



**New-UDRadio**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Label | String | The label to show next to the radio. | false |
| Disabled | SwitchParameter | Whether the radio is disabled. | false |
| Value | String | The value of the radio. | false |
| LabelPlacement | String | The position to place the label in relation to the radio. | false |

