---
description: List component for Universal Dashboard.
---

# List

Lists are continuous, vertical indexes of text or images.

Lists are a continuous group of text or images. They are composed of items containing primary and supplemental actions, which are represented by icons and text.

## List

![](<../../../../.gitbook/assets/image (51).png>)

```
New-UDList -Content {
    New-UDListItem -Label 'Inbox' -Icon (New-UDIcon -Icon envelope -Size 3x) -SubTitle 'New Stuff'
    New-UDListItem -Label 'Drafts' -Icon (New-UDIcon -Icon edit -Size 3x) -SubTitle "Stuff I'm working on "
    New-UDListItem -Label 'Trash' -Icon (New-UDIcon -Icon trash -Size 3x) -SubTitle 'Stuff I deleted'
    New-UDListItem -Label 'Spam' -Icon (New-UDIcon -Icon bug -Size 3x) -SubTitle "Stuff I didn't want"
}
```

## OnClick Event Handler

You can define an action to take when an item is clicked by using the `-OnClick` parameter of `New-UDListItem`.

```
New-UDList -Content {
    New-UDListItem -Label 'Inbox' -Icon (New-UDIcon -Icon envelope -Size 3x) -SubTitle 'New Stuff'
    New-UDListItem -Label 'Drafts' -Icon (New-UDIcon -Icon edit -Size 3x) -SubTitle "Stuff I'm working on "
    New-UDListItem -Label 'Trash' -Icon (New-UDIcon -Icon trash -Size 3x) -SubTitle 'Stuff I deleted'
    New-UDListItem -Label 'Spam' -Icon (New-UDIcon -Icon bug -Size 3x) -SubTitle "Stuff I didn't want" -OnClick {
        Show-UDToast -Message 'Clicked'
    }
}
```

## API

* [**New-UDList**](../../../../cmdlets/New-UDList.txt)****
* ****[**New-UDListItem**](../../../../cmdlets/New-UDListItem.txt)****
