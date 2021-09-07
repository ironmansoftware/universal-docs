---
description: >-
  A transfer list (or "shuttle") enables the user to move one or more list items
  between lists.
---

# Transfer List

{% hint style="warning" %}
This feature will be available in PowerShell Universal 2.3
{% endhint %}

## Simple Transfer List

Create a simple transfer list.

```text
New-UDTransferList -Item {
    New-UDTransferListItem -Name 'test1' -Value 1
    New-UDTransferListItem -Name 'test2' -Value 2
    New-UDTransferListItem -Name 'test3' -Value 3
    New-UDTransferListItem -Name 'test4' -Value 4
    New-UDTransferListItem -Name 'test5' -Value 5
} 
```

![](../../../../.gitbook/assets/image%20%28236%29.png)

## Transfer List Value on Change

Use the `OnChange` event handler to get the value of the selected items. 

```text
New-UDTransferList -Item {
    New-UDTransferListItem -Name 'test1' -Value 1
    New-UDTransferListItem -Name 'test2' -Value 2
    New-UDTransferListItem -Name 'test3' -Value 3
    New-UDTransferListItem -Name 'test4' -Value 4
    New-UDTransferListItem -Name 'test5' -Value 5
} -OnChange {
    Show-UDToast ($EventData | ConvertTo-Json)
}
```

## Transfer List in a Form

Transfer lists can be used within forms and steppers. 

```text
New-UDForm -Content {
    New-UDTransferList -Item {
        New-UDTransferListItem -Name 'test1' -Value 1
        New-UDTransferListItem -Name 'test2' -Value 2
        New-UDTransferListItem -Name 'test3' -Value 3
        New-UDTransferListItem -Name 'test4' -Value 4
        New-UDTransferListItem -Name 'test5' -Value 5
    }
} -OnSubmit {
    Show-UDToast ($EventData | ConvertTo-Json)
}
```

