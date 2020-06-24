---
description: Button component for Universal Dashboard
---

# Button

Buttons allow users to take actions, and make choices, with a single tap.

## Contained Button

Contained buttons are high-emphasis, distinguished by their use of elevation and fill. They contain actions that are primary to your app.

```text
 New-UDButton -Variant 'contained' -Text 'Default'
```

## Outlined Button

Outlined buttons are medium-emphasis buttons. They contain actions that are important, but aren’t the primary action in an app.

```text
New-UDButton -Variant 'outlined' -Text 'Default' 
```

## Buttons with icons and label

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

