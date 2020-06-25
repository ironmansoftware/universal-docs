---
description: Button component for Universal Dashboard
---

# Button

Buttons allow users to take actions, and make choices, with a single tap.

## Contained Button

![](../../../.gitbook/assets/image%20%2875%29.png)

Contained buttons are high-emphasis, distinguished by their use of elevation and fill. They contain actions that are primary to your app.

```text
 New-UDButton -Variant 'contained' -Text 'Default'
```

## Outlined Button

![](../../../.gitbook/assets/image%20%2836%29.png)

Outlined buttons are medium-emphasis buttons. They contain actions that are important, but aren’t the primary action in an app.

```text
New-UDButton -Variant 'outlined' -Text 'Default' 
```

## Buttons with icons and label

![](../../../.gitbook/assets/image%20%2882%29.png)

Sometimes you might want to have icons for certain button to enhance the UX of the application as we recognize logos more easily than plain text. For example, if you have a delete button you can label it with a dustbin icon.

```text
New-UDButton -Icon (New-UDIcon -Icon trash) -Text 'Delete'
```

## Buttons with event handlers

You can specify a script block to execute when the button is clicked

```text
New-UDButton -Text 'Message Box' -OnClick {
    Show-UDToast -Message 'Hello, world!'
}
```



**New-UDButton**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Text | String | The text to show within the button. | false |
| Icon | Object | An icon to show within the button. Use New-UDIcon to create an icon for this parameter. | false |
| Variant | String | The variant type for this button. | false |
| IconAlignment | String | How to align the icon within the button. | false |
| FullWidth | SwitchParameter | Whether the button takes the full width of the it's container. | false |
| OnClick | Endpoint | The action to take when the button is clicked. | false |
| Size | String | The size of the button. | false |
| Style | Hashtable | Styles to apply to the button. | false |
| Href | String | A URL that the user should be redirected to when clicking the button. | false |
| Id | String | The ID of the component. It defaults to a random GUID. | false |

