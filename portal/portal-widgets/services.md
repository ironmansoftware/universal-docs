---
description: Services available in portal components.
---

# Services

## JavaScript

The JavaScript runtime can be accessed with the JavaScript service. It allows for executing JavaScript on the client and optionally returning a response.&#x20;

```powershell
function OnClick {
    #Don't return a value    
    $JavaScript.InvokeVoid("alert('Hello!')")
    
    #Return a value
    $Value = $JavaScript.Invoke("'String'")
    $Message.Success($Value)
}
```

## Messages&#x20;

The message service is used to display messages to the end user. It is based on the `IMessageService`. You can find more information [here](https://antblazor.com/en-US/components/message#API).

```powershell
function OnClick {
   $Message.Success("Hello!")
}
```

## Notifications

The notification service is used to display messages the include more information that the message service. You can customize the title, message and icon. You can find more information [here](https://antblazor.com/en-US/components/notification).

```powershell
function OnClick {
    $Config = [AntDesign.NotificationConfig]::new()
    $Config.Message = "Title" 
    $Config.Description = "This is the body of the notification"
    $Notification.Open($Config)
}
```

## Navigation

The navigation service can be used to move between portal pages, admin pages and external pages. The navigation service is an instance of [NavigationManager](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.components.navigationmanager?view=aspnetcore-8.0).

```powershell
function OnClick {
    $Navigation.NavigateTo("/portal/page/name")
}
```
