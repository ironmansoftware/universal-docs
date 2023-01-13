---
description: Interaction features of Universal Dashboard
---

# Interaction

Universal Dashboard enables the ability to create interactive websites with PowerShell. There are several cmdlets that have been implemented to provide feedback to the user, update components and read the state of components.

## Clipboard

You can set string data into the user's clipboard with `Set-UDClipboard`.

```powershell
New-UDButton -Text 'Clipboard' -OnClick {
    Set-UDClipboard -Data 'Hello, there!'
}
```

#### API

* [Set-UDClipboard](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-UDClipboard.txt)

## Downloads

You can start a download within the user's browser by using `Start-UDDownload`. Due to security of web browsers, the user will need to take an action (like click a button) to allow the download to take place. `Start-UDDownload` is not suited for large file downloads.

```powershell
New-UDButton -Text 'Download' -OnClick {
    Start-UDDownload -StringData 'Hello, World!'
}
```

## Event Handlers

Many components support event handlers in the form of script blocks. You may also see these referred to as endpoints as that is what they were called in Universal Dashboard v2. These event handlers allow you to invoke PowerShell scripts when certain actions take place on the page.&#x20;

For example, you may have a button click that calls an event handler. This button will show a toast when clicked. You can include any valid PowerShell cmdlet within the event handler code.&#x20;

```powershell
New-UDButton -Text 'Click Me' -OnClick {
   Show-UDToast 'Hello!'
}
```

### Variable Scope

Variables are automatically scoped into event handlers. You will be able to access variables that you define outside of the variable within the event handler.&#x20;

```powershell
$MyVariable = "Hello!"
New-UDButton -Text 'Click Me' -OnClick {
   Show-UDToast $MyVariable
}
```

### Event Data&#x20;

Some event handlers handlers will provide data as a string or as a hashtable. This depends on the event handler you are using. For example, the `New-UDButton` `-OnClick` event handler does not provide any data. On the other hand, the `New-UDSelect` `-OnChange` will provider event data.&#x20;

You can access the event data by using the `$Body` variable to access the data as a string (sometimes formatted as JSON) or as a hashtable by using the `$EventData` variable.&#x20;

```powershell
New-UDSelect -Option {
    New-UDSelectOption -Name 'One' -Value 1
    New-UDSelectOption -Name 'Two' -Value 2
    New-UDSelectOption -Name 'Three' -Value 3
} -OnChange { Show-UDToast -Message $EventData }
```

## Forms

### Submit a Form

You can force a form to submit using the `Invoke-UDForm` cmdlet. You can optionally chose to enforce validation by including the `-Validate` parameter.

```powershell
New-UDForm -Id 'form' -Content {
   New-UDTextbox -Id 'Text' -Label 'Submit Me'
} -OnSubmit {
   Show-UDToast "Hello!"
}

New-UDButton -Text "Submit Form" -OnClick {
   Invoke-UDForm -Id 'form'
}
```

### Validate a Form

You can force a form to validate by using `Test-UDForm`.

```powershell
New-UDForm -Id 'form' -Content {
   New-UDTextbox -Id 'Text' -Label 'Submit Me'
} -OnSubmit {
   Show-UDToast "Hello!"
} -OnValidate {
   New-UDValidationResult
}

New-UDButton -Text "Submit Form" -OnClick {
   Test-UDForm -Id 'form'
}
```

## JavaScript

You can invoke JavaScript from PowerShell by using the `Invoke-UDJavaScript` cmdlet.

```powershell
New-UDButton -Text 'Alert Me' -OnClick {
    Invoke-UDJavaScript -JavaScript 'alert("Hello!")'
}
```

#### **API**

* [Invoke-UDJavaScript](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Invoke-UDJavaScript.txt)

## Toast

### Show a toast

You can use the `Show-UDToast` cmdlet to create a toast message that will appear on the end user's webpage. It happens over a websocket and will show the toast immediately as it is called.

```powershell
Show-UDToast -Message 'Hello, World!'
```

### Show as toast with an Icon

Toasts support icons as strings. You can use all the FontAwesome v5 icons.&#x20;

```powershell
Show-UDToast -Icon "Ad" -Message "Test"
```

### Hide a toast

Hides a toast based on the specified ID.

```powershell
Show-UDToast -Message 'Hello, World!' -Id 'Toast' -Duration 30000

New-UDButton -Text 'Click' -OnClick {
    Hide-UDToast -Id 'Toast'
}
```

### API

* [Show-UDToast](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Show-UDToast.txt)
* [Hide-UDToast](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Hide-UDToast.txt)

## Redirect

You can redirect users to different pages using the `Invoke-UDRedirect` cmdlet. It happens over a websocket and will redirect as soon as the cmdlet is called.

```powershell
Invoke-UDRedirect http://www.ironmansoftware.com
```

`Invoke-UDRedirect` will automatically redirect to pages in the dashboard when using a relative path.&#x20;

```powershell
Invoke-UDRedirect '/page1' 
```

If you'd like to redirect to a local path outside of the dashboard, you can use the `-Native` parameter.&#x20;

```powershell
Invoke-UDRedirect '/publishedFolder/test.txt' -Native
```

#### API

* [Invoke-UDRedirect](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Invoke-UDRedirect.txt)

## Modal

You can open a modal using the `Show-UDModal` cmdlet. It will open as soon as you call it. You can include whatever components you like within the modal.

Read more about [Modals here](components/feedback/modal.md).

## Managing Component State

You can manage component state dynamically by using the UDElement commands.

### Getting Component State

You can receive the state of an element using `Get-UDElement` . The state will be returned as a hashtable. This is primarily useful for input components.

```powershell
$Value = (Get-UDElement -Id 'txtExample').value
```



### Setting Component State

Alternatively, you can set component state using `Set-UDElement` . You will need to specify an ID and a hashtable of properties to set on the component. All built in components support Set-UDElement.

```powershell
New-UDTextbox -Id 'textbox'

New-UDButton -Text 'Click' -OnClick {
    Set-UDElement -Id 'textbox' -Properties @{
        Value = 'My Value'
    }
}
```

### Removing a Component

You can remove components from the page using `Remove-UDElement` . The component will no longer appear on the page.

```powershell
Remove-UDComponent -Id 'txtExample'
```

### Adding a component

Add a child component to an existing parent component.

```powershell
New-UDElement -Id 'myDiv' -Tag div

New-UDButton -Text 'Click' -OnClick {
    Add-UDElement -ParentId 'myDiv' -Content {
        New-UDTypography -Text 'Hi'
    }
}
```

### Clear a component

You can remove all the children components from an component by using `Clear-UDElement`.

```powershell
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

### Reloading a Component

Some components support reloading. You can trigger a reload of a component using `Sync-UDElement`.

```powershell
New-UDDynamic -Id 'reloadMe' -Content {
    Get-Date
}

New-UDButton -Text 'Reload' -OnClick {
    Sync-UDElement -Id 'reloadMe'
}
```

### Select a component

You can select a component with `Select-UDElement`.

```powershell
New-UDElement -Id 'txt' -Tag input -Properties @{ type = text }

New-UDButton -Text 'Select' -OnClick {
    Select-UDElement -Id 'txt' -ScrollToElement
}
```

## PowerShell Host Integration

Dashboards integrate directly with the PowerShell host to provide features based on standard cmdlets.&#x20;

### Read-Host

Using the `Read-Host` cmdlet will cause a dialog to show on the user's dashboard. The text entered will be returned by the cmdlet.&#x20;

```powershell
$Text = Read-Host 'Enter Some Text'
Show-UDToast $Text
```

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

### Get-Credential

Using `Get-Credential` will cause a dialog to show that accepts a username and password. A `PSCredential` object will be returned from the cmdlet.&#x20;

```powershell
Get-Credential -UserName "adam"
```

<figure><img src="../../.gitbook/assets/image (2) (4).png" alt=""><figcaption></figcaption></figure>

### Write-Progress

Cmdlets that use the progress stream or the use of the `Write-Progress` cmdlet will result in a progress dialog being shown. The popup will show the activity, percent completed and current operation.

```powershell
1..100 | ForEach-Object {
    Write-Progress -PercentComplete $_ -Activity 'Processing...' -CurrentOperation "User $_"
    Start-Sleep -Milliseconds 500
}
```

<figure><img src="../../.gitbook/assets/image (1) (5).png" alt=""><figcaption></figcaption></figure>

You can disable the Write-Progress integration by setting the `$ProgressPreference` to `SilentlyContinue`.

```powershell
$ProgressPreference = 'SilentlyContinue'
```

### Prompt For Choice

You can use the `$Host.UI.PromptForChoice` function to display a multi-select dialog.&#x20;

```powershell
$Title = "Welcome"
$Info = "Just to Demo Prompt for Choice"

$options = [System.Management.Automation.Host.ChoiceDescription[]] @("Power", "Shell", "Quit")
[int]$defaultchoice = 2
$opt = $host.UI.PromptForChoice($Title , $Info , $Options, $defaultchoice)
switch ($opt) {
    0 { Show-UDToast "Power" }
    1 { Show-UDToast "Shell" }
    2 { Show-UDToast "Good Bye!!!" }
}
```

<figure><img src="../../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

## API

* [Get-UDElement](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Get-UDElement.txt)
* [Set-UDElement](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-UDElement.txt)
* [Clear-UDElement](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Clear-UDElement.txt)
* [Remove-UDElement](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Remove-UDElement.txt)
* [Sync-UDElement](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Sync-UDElement.txt)
* [Select-UDElement](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Select-UDElement.txt)
