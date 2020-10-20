---
description: Typography component for Universal Dashboard
---

# Typography

Use typography to present your design and content as clearly and efficiently as possible.

Too many type sizes and styles at once can spoil any layout. A typographic scale has a limited set of type sizes that work well together along with the layout grid.

![](../../../.gitbook/assets/image%20%2876%29.png)

## All Typography Types

```text
@("h1", "h2", "h3", "h4", "h5", "h6", "subtitle1", "subtitle2", "body1", "body2", 
"caption", "button", "overline", "srOnly", "inherit", 
"display4", "display3", "display2", "display1", "headline", "title", "subheading") | ForEach-Object {
    New-UDTypography -Variant $_ -Text $_ -GutterBottom
    New-UDElement -Tag 'p' -Content {}
}
```

## Colored Text

You can use the `-Style` parameter to define colors for your text. 

```text
New-UDTypography -Text 'My Text' -Style @{ color = 'blue' }
```

**New-UDTypography**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | String | The ID of the component. It defaults to a random GUID. | false |
| Variant | String | The type of text to display. | false |
| Text | String | The text to format. | false |
| Content | ScriptBlock | The content to format. | false |
| Style | Hashtable | A set of CSS styles to apply to the typography. | false |
| ClassName | String | A CSS className to apply to the typography. | false |
| Align | String | How to align the typography. | false |
| GutterBottom | SwitchParameter | The gutter bottom. | false |
| NoWrap | SwitchParameter | Disables text wrapping. | false |
| Paragraph | SwitchParameter | Whether this typography is a paragraph. | false |

