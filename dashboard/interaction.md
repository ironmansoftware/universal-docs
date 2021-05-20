---
description: Interaction features of Universal Dashboard
---

# Interaction

Universal Dashboard enables the ability to create interactive websites with PowerShell. There are several cmdlets that have been implemented to provide feedback to the user, update components and read the state of components.

## Toast

You can use the `Show-UDToast` cmdlet to create a toast message that will appear on the end user's webpage. It happens over a websocket and will show the toast immediately as it is called.

```text
Show-UDToast -Message 'Hello, World!'
```

### API

**Show-UDToast**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Message | string | The message to display | true |
| MessageColor | DashboardColor | The color of the message to display | false |
| MessageSize | string | The size of the message to display | false |
| Duration | int | The number of milliseconds to display the message. Defaults to 1000 | false |
| Title | string | A title to display above the message.  | false |
| TitleColor | DashboardColor | The color of the title. | false |
| TitleSize | string | The size of the title. | false |
| Id | string | The ID of this toast. | false |
| BackgroundColor | DashboardColor | The background color of the toast. | false |
| Theme | string | Light or dark theme. | false |
| Position | string | The position of the toast. | false |
| HideCloseButton | Switch | Hide the close button to prevent the user from hiding the toast. | false |
| CloseOnClick | Switch | Close the toast when it is clicked. | false |
| CloseOnEscape | Switch | Close the toast when escape is pressed. | false |
| ReplaceToast | Switch | Replace an existing toast if one is already shown. Otherwise, show both. | false |
| Balloon | Switch | Balloon style toast.  | false |
| Overlay | Switch | Display an overlay behind the toast | false |
| OverlayClose | Switch | Allow the user to close the overlay | false |
| OverlayColor | DashboardColor | The color of the overlay. | false |
| TransitionIn | string | The transition to use when the toast is appearing. | false |
| TransitionOut | string | The transition to use when the toast is disappearing. | false |
| Broadcast | Switch | Show the toast to all users. | false |

## Redirect

You can redirect users to different pages using the `Invoke-UDRedirect` cmdlet. It happens over a websocket and will redirect as soon as the cmdlet is called.

```text
Invoke-UDRedirect http://www.ironmansoftware.com
```

## Modal

You can open a modal using the `Show-UDModal` cmdlet. It will open as soon as you call it. You can include whatever components you like within the modal.

Read more about [Modals here](components/feedback/modal.md).

## Getting Component State

You can receive the state of an element using `Get-UDElement` . The state will be returned as a hashtable. This is primarily useful for input components.

```text
$Value = (Get-UDElement -Id 'txtExample').value
```

## Setting Component State

Alternatively, you can set component state using `Set-UDElement` . You will need to specify an ID and a hashtable of properties to set on the component. All built in components support Set-UDElement.

```text
New-UDTextbox -Id 'textbox'

New-UDButton -Text 'Click' -OnClick {
    Set-UDElement -Id 'textbox' -Properties @{
        Value = 'My Value'
    }
}
```

## Removing a Component

You can remove components from the page using `Remove-UDElement` . The component will no longer appear on the page.

```text
Remove-UDComponent -Id 'txtExample'
```

## Adding a component

Add a child component to an existing parent component. 

```text
New-UDElement -Id 'myDiv' -Tag div

New-UDButton -Text 'Click' -OnClick {
    Add-UDElement -ParentId 'myDiv' -Content {
        New-UDTypography -Text 'Hi'
    }
}
```

