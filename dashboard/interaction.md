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

## Removing a Component

You can remove components from the page using `Remove-UDElement` . The component will no longer appear on the page. 

```text
Remove-UDComponent -Id 'txtExample'
```

