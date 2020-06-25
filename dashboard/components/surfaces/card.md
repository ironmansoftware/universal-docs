---
description: Card component for Universal Dashboard
---

# Card

**Cards contain content and actions about a single subject.**

Cards are surfaces that display content and actions on a single topic. They should be easy to scan for relevant and actionable information. Elements, like text and images, should be placed on them in a way that clearly indicates hierarchy.

## Simple Card

Although cards can support multiple actions, UI controls, and an overflow menu, use restraint and remember that cards are entry points to more complex and detailed information.

![](../../../.gitbook/assets/image%20%2856%29.png)

```text
New-UDCard -Title 'Simple Card' -Content {
    "This is some content"
}
```



**New-UDCard**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| ClassName | String | A CSS class to assign to this card. | false |
| ShowToolBar | SwitchParameter | Whether to show the toolbar for this card. | false |
| ToolBar | Object | The toolbar for this card. Use New-UDCardToolbar to create a toolbar. | false |
| Header | Object | The header for this card. The header typically contains a title for the card. Use New-UDCardHeader to create a header. | false |
| Body | Object | The body for this card. This is the main content for the card. Use New-UDCardHeader to create a body. | false |
| Expand | Object | Th expand content for this card. Expand content is show when the user clicks the expansion button. Use New-UDCardExpand to create an expand. | false |
| Footer | Object | The footer for this card. Footer contents typically contain actions that are relavent to the card. Use New-UDCardFooter to create a footer. | false |
| Style | Hashtable | Styles to apply to the card. | false |
| Elevation | Int32 | The amount of elevation to provide the card. The more elevation, the more it will appear the card is floating off the page. | false |
| Title | String | A title for the card. | false |
| TitleAlignment | String | The alignment for the title. | false |
| Content | ScriptBlock | The content of the card. | false |
| Image | String | An image to show in the card. | false |

