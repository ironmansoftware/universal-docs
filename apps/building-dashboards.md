---
description: Apps are the root component for your web page.
---

# Apps

## Create An App

The first step is to create an app in PowerShell Universal. This is the container for all your pages and components for your app website. We recommend running apps in external environments, like PowerShell 7, to ensure they are isolated from the rest of the server. To create an app, click Apps \ Apps and then Create New App.&#x20;

You will need to provide a unique name and URL for the app when creating it. All other properties are optional. After creating the app, you can edit the app code. For example, try adding a component to your app.&#x20;

```powershell
New-UDApp -Content {
   New-UDButton -Text 'Click Me' -OnClick {
       Show-UDToast "Ouch!"
   }
}
```

Once you've saved your app, you can click the globe icon to view the result. Clicking the button will display a toast message in your browser.

## New-UDApp

The top-level cmdlet for dashboards is `New-UDApp`. You need to call it when returning an app. You can use it with or without pages.

#### Content

The content of the app is a series of components to display on the page. It's a script block that will return all the components in the order they will be rendered on the page. You can use the Grid component to layout items and display things like text with typography.

```powershell
New-UDApp -Title 'My New Dashboard' -Content {
    New-UDTypography -Text 'Hello!'
}
```

## Header Customization

You can customize the header of the app using several parameters.

To change the navigation layout, use the `-Navigation` and `-NavigationLayout` parameters.

```powershell
New-UDApp -Content {
} -Navigation (
    New-UDList -Children {
        New-UDListItem -Label "Home"
        New-UDListItem -Label "Getting Started" -Children {
            New-UDListItem -Label "Installation" -OnClick {}
            New-UDListItem -Label "Usage" -OnClick {}
            New-UDListItem -Label "FAQs" -OnClick {}
            New-UDListItem -Label "System Requirements" -OnClick {}
            New-UDListItem -Label "Purchasing" -OnClick {}
        }
    }
) -NavigationLayout permanent
```

## Components

Components are the individual widgets that you can place on you app. There are components for displaying data, taking user input, adding text and images and more. Components can be downloaded as PowerShell modules and added to your app.

Components are be caused using the standard verb-name syntax for any PowerShell cmdlet.

```powershell
New-UDPage -Content {
    New-UDTextbox
}
```

Learn more about [components here](building-dashboards.md#components).

## Pages

You can specify multiple pages within an app. Each page defines a route. As for v3, all pages are dynamic. PowerShell will execute on each page load to render the new page. Since UD is a single page application, the web browser does not need to refresh the entire web page when navigating between the different app pages.

```powershell
$Pages = @()
$Pages += New-UDPage -Name 'My Home Page' -Content {}
$Pages += New-UDPage -Name 'Diagnostics' -Content {}
New-UDApp -Pages $Pages -Title 'Dashboard'
```

Learn more about [Pages here](building-dashboards.md#pages).

## Built-in Variables

Built-in variables can be found on the [variables page](../platform/variables.md#dashboards).

## Debugging

{% hint style="info" %}
You can also use the [Debugging Tools](../development/debugging-scripts.md#integrated-debugger) with apps.
{% endhint %}

When building an app, you will likely run into issues with cmdlet calls or syntax. Apps will auto reload as you make changes to the app files. If an app fails to start, you can navigate to the admin page, click Apps and click the Info button next to your app.

The Log tab will show all the logging coming from the PowerShell execution from within in your app. This should allow you to easily see errors and warnings coming from your app.

You can use `Write-Debug` to add additional log messages to your app. To enable debug logging, you will have to set the `$DebugPreference` variable at the top of your app script.

```powershell
$DebugPreference = 'Continue'
```

## Menu

You can customize the appmenu by using the `-Menu` parameter.

```powershell
New-UDApp -Title 'App' -Content {

} -Menu {
    New-UDMenuItem -Text 'Profile' -OnClick {
        Show-UDModal -Content {
            New-UDTypography -Text 'Welcome to your profile!'
        }
    }
}
```

## Starting and Stopping Apps

Similar to jobs, apps can run in separate PowerShell processes. You can start and stop an app process by clicking the Start or Stop button from the Apps page.

## Persistent Runspaces

Persistent runspaces allow you to maintain runspace state within your app event handlers. This is important for users that perform some sort of initialization within their endpoints that they do not want to execute on subsequent calls.

By default, runspaces will be reset after each execution. This will cause variables, modules and functions defined during the execution of an endpoint.

To enable persistent runspaces, you will need to configure an [environment ](../config/environments.md)for your API. Set the `-PersistentRunspace` parameter to enable this feature. This is configured in the `environments.ps1` script.

```
New-PSUEnvironment -Name 'Env' -Path 'powershell.exe' -PersistentRunspace
```

You will need to ensure that the environment is used by the app.

## Automatically Granting App Tokens

You can automatically grant app tokens to users that visit apps. This is useful if you want to invoke the management API for PowerShell Universal from within an app. Your app will need to have authentication enabled and you will have to use the `-GrantAppToken` switch parameter on `New-PSUDashboard`.

```
New-PSUApp -Name 'App' -BaseUrl '/' -Authenticated -GrantAppToken
```

From within your app, you can now invoke the management API without having to worry about app token management. The API will be invoked in the context of the user that is visiting the app.

```
New-UDApp -Title "Hello, World!" -Content {
    New-UDButton -Text 'Job' -OnClick {
        Invoke-UAScript -Name 'Test.ps1'
    }
}
```

## Disable Error Toasts

By default, apps will display a toast message when an error is generated within an endpoint script. To avoid this behavior, you can use the `-DisableErrorToast` parameter of `New-UDApp`

```
New-PSUApp -Name 'App' -BaseUrl '/' -Authenticated -DisableErrorToast
```

```
New-UDApp -Title "Hello, World!" -Content {
    New-UDButton -Text 'Job' -OnClick {
        throw "Exception
    }
} 
```

## Disable Startup Logging

When starting an app, information about the variables and modules is displayed within the app log. If you wish to suppress this information, you can use the `-DisableStartupLogging` parameter.

```
New-PSUApp -Name 'App' -BaseUrl '/' -DisableStartupLogging
```

