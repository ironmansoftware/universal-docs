---
description: About User Interfaces in PowerShell Universal.
---

# About

Apps are individual websites created with PowerShell Universal. You can define settings for an app and start and stop the app from within the Universal administrative interface.

## Adding an App

Apps can be added to Universal using the Add App button from the User Interfaces / Apps page.

**Name**

Name is displayed throughout the UI and returned from the Universal cmdlets.

**Base URL**

The base URL is the URL that you will access to view this app. This URL needs to be unique within this instance. You can specify the `/` root URL if you wish. You will have to visit `/admin` to login to the administrative page if you set the dashboard to the root URL.

**File Name**

The full file name to the dashboard file. This file needs to return an app using New-UDApp.

**Environment**

The [environment ](../config/environments.md)to run the app within.

**Authentication**

Enables authentication for the app.

**Roles**

Defines the role that is required to access the app.

**AutoStart**

Determines whether the app should start (or restart) when the server starts or changes are made to the app files.

![](<../.gitbook/assets/image (2) (1) (1).png>)

## Starting and Stopping Apps

Similar to jobs, apps run in separate PowerShell processes. You can start and stop an app process by clicking the Start or Stop button from the Apps page.

## Viewing Diagnostic Information

You can view diagnostic information for an app by clicking the Info button on the Apps page. This will show your start information for the app as well as any error that were encountered when starting the app.

## Viewing the Apps

You can view the app by clicking the View button. This will take you to the Base URL for the app.

## Executing Commands with the App

On the app information page, click on the Console tab to view the console. The console allows you to run scripts from within the app runspace so you can better debug the state of your script. You can evaluate variables and run commands that are available to the app. You will be running in the context of your user in regards to the runspace but the process will be running as the service account user.

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

When starting an app, information about the variables and modules is displayed within the app log. If you wish to suppress this information, you can use the `-DisableStartupLogging` parameter.&#x20;

```
New-PSUApp -Name 'App' -BaseUrl '/' -DisableStartupLogging
```

## Variables Available in Apps

Built-in variables are listed on the [variables page.](../platform/variables.md#dashboards)
