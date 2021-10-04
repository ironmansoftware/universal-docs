---
description: Interaction features of Universal Dashboard
---

# Interaction

Universal Dashboard enables the ability to create interactive websites with PowerShell. There are several cmdlets that have been implemented to provide feedback to the user, update components and read the state of components.

## Clipboard

You can set string data into the user's clipboard with `Set-UDClipboard`.

```text
New-UDButton -Text 'Clipboard' -OnClick {
    Set-UDClipboard -Data 'Hello, there!'
}
```

#### API

**Set-UDClipboard**

| **Name** | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Data | string | The content to set to the clipboard | true |
| ToastOnSuccess | Switch | Shows a toast if the data was successfully set in the clipboard | false |
| ToastOnError | Switch | Shows as toast if the data was unsuccessfully set in the clipboard | false |

## JavaScript

You can invoke JavaScript from PowerShell by using the `Invoke-UDJavaScript` cmdlet.

```text
New-UDButton -Text 'Alert Me' -OnClick {
    Invoke-UDJavaScript -JavaScript 'alert("Hello!")'
}
```

#### **API**

**Invoke-UDJavaScript**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| **JavaScript** | string | The JavaScript to invoke. | true |

## Toast

### Show a toast

You can use the `Show-UDToast` cmdlet to create a toast message that will appear on the end user's webpage. It happens over a websocket and will show the toast immediately as it is called.

```text
Show-UDToast -Message 'Hello, World!'
```

### Hide a toast

Hides a toast based on the specified ID.

```text
Show-UDToast -Message 'Hello, World!' -Id 'Toast' -Duration 30000

New-UDButton -Text 'Click' -OnClick {
    Hide-UDToast -Id 'Toast'
}
```

### API

**Show-UDToast**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Message | string | The message to display | true |
| MessageColor | DashboardColor | The color of the message to display | false |
| MessageSize | string | The size of the message to display | false |
| Duration | int | The number of milliseconds to display the message. Defaults to 1000 | false |
| Title | string | A title to display above the message. | false |
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
| Balloon | Switch | Balloon style toast. | false |
| Overlay | Switch | Display an overlay behind the toast | false |
| OverlayClose | Switch | Allow the user to close the overlay | false |
| OverlayColor | DashboardColor | The color of the overlay. | false |
| TransitionIn | string | The transition to use when the toast is appearing. | false |
| TransitionOut | string | The transition to use when the toast is disappearing. | false |
| Broadcast | Switch | Show the toast to all users. | false |
| Persistent | Switch | Persist the toast until dismissed. | false |

**Hide-UDToast**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| **Id** | string | The ID of the toast to hide. | true |

## Redirect

You can redirect users to different pages using the `Invoke-UDRedirect` cmdlet. It happens over a websocket and will redirect as soon as the cmdlet is called.

```text
Invoke-UDRedirect http://www.ironmansoftware.com
```

#### API

**Invoke-UDRedirect**

| **Name** | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Url | string | The URL to redirect the user to. | true |
| OpenInNewWindow | Switch | Open the URL in a new window or tab. | false |

## Modal

You can open a modal using the `Show-UDModal` cmdlet. It will open as soon as you call it. You can include whatever components you like within the modal.

Read more about [Modals here](components/feedback/modal.md).

## Managing Component State

You can manage component state dynamically by using the UDElement commands.

### Getting Component State

You can receive the state of an element using `Get-UDElement` . The state will be returned as a hashtable. This is primarily useful for input components.

```text
$Value = (Get-UDElement -Id 'txtExample').value
```

#### API

**Get-UDElement**

| **Name** | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string | The ID of the component to receive. | true |

### Setting Component State

Alternatively, you can set component state using `Set-UDElement` . You will need to specify an ID and a hashtable of properties to set on the component. All built in components support Set-UDElement.

```text
New-UDTextbox -Id 'textbox'

New-UDButton -Text 'Click' -OnClick {
    Set-UDElement -Id 'textbox' -Properties @{
        Value = 'My Value'
    }
}
```

#### API

**Set-UDElement**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string | The ID of the component to set. | true |
| Properties | Hashtable | Properties to set on the component | false |
| Broadcast | Switch | Set the properties of a component for all users. | false |
| Content | ScriptBlock | The content of the component to set. | false |

### Removing a Component

You can remove components from the page using `Remove-UDElement` . The component will no longer appear on the page.

```text
Remove-UDComponent -Id 'txtExample'
```

#### API

**Remove-UDElement**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string | The ID of the component to remove. | true |

### Adding a component

Add a child component to an existing parent component.

```text
New-UDElement -Id 'myDiv' -Tag div

New-UDButton -Text 'Click' -OnClick {
    Add-UDElement -ParentId 'myDiv' -Content {
        New-UDTypography -Text 'Hi'
    }
}
```

#### API

**Add-UDElement**

| **Name** | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| ParentId | string | The ID of the component to add a child to. | true |
| Content | ScriptBlock | The child content to add. | true |
| Broadcast | Switch | Whether to add the child component to all users. | false |

#### Clear a component

You can remove all the children components from an component by using `Clear-UDElement`.

```text
New-UDElement -Id 'myDiv' -Tag div

New-UDButton -Text 'Click' -OnClick {
    Add-UDElement -ParentId 'myDiv' -Content {
        New-UDTypography -Text 'Hi'
    }
    Add-UDElement -ParentId 'myDiv' -Content {
        New-UDTypography -Text 'Hi'
    }
    Add-UDElement -ParentId 'myDiv' -Content {
        New-UDTypography -Text 'Hi'
    }
}

New-UDButton -Text 'Clear' -OnClick {
    Clear-UDElement -Id 'myDiv'
}
```

#### API

**Clear-UDElement**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string | The ID of the component to clear. | true |

### Reloading a Component

Some components support reloading. You can trigger a reload of a component using `Sync-UDElement`.

```text
New-UDDynamic -Id 'reloadMe' -Content {
    Get-Date
}

New-UDButton -Text 'Reload' -OnClick {
    Sync-UDElement -Id 'reloadMe'
}
```

#### API

**Sync-UDElement**

| Name | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string | The ID of the component to reload. | true |
| Broadcast | Switch | Whether to reload the component for all users. | false |

### Select a component

You can select a component with `Select-UDElement`.

```text
New-UDElement -Id 'txt' -Tag input -Properties @{ type = text }

New-UDButton -Text 'Select' -OnClick {
    Select-UDElement -Id 'txt' -ScrollToElement
}
```

#### API

**Select-UDElement**

| **Name** | Type | Description | Required |
| :--- | :--- | :--- | :--- |
| Id | string | The ID of the element to select | true |
| ScrollToElement | Switch | Whether to scroll the user's window to the element | false |

