---
description: List component for Universal Dashboard.
---

# List

Lists are continuous, vertical indexes of text or images.

Lists are a continuous group of text or images. They are composed of items containing primary and supplemental actions, which are represented by icons and text.

## List 

![](../../../.gitbook/assets/image%20%2851%29.png)

```text
New-UDList -Content {
    New-UDListItem -Label 'Inbox' -Icon (New-UDIcon -Icon envelope -Size 3x) -SubTitle 'New Stuff'
    New-UDListItem -Label 'Drafts' -Icon (New-UDIcon -Icon edit -Size 3x) -SubTitle "Stuff I'm working on "
    New-UDListItem -Label 'Trash' -Icon (New-UDIcon -Icon trash -Size 3x) -SubTitle 'Stuff I deleted'
    New-UDListItem -Label 'Spam' -Icon (New-UDIcon -Icon bug -Size 3x) -SubTitle "Stuff I didn't want"
}
```



**New-UDList**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Children | ScriptBlock | The items in the list. | false |
| SubHeader | String | Text to show within the sub header. | false |



**New-UDListItem**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| AvatarType | String | The type of avatar to show within the list item. | false |
| OnClick | Endpoint | A script block to execute when the list item is clicked. | false |
| Label | String | The label to show within the list item. | false |
| Children | ScriptBlock | Nested list items to show underneath this list item. | false |
| SubTitle | String | The subtitle to show within the list item. | false |
| Icon | Object | The icon to show within the list item. | false |
| Source | String | Parameter description | false |
| SecondaryAction | ScriptBlock | The secondary action to issue with this list item. | false |

