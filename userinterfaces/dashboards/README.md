# Dashboards

Dashboards are individual websites created with Universal Dashboard. You can define settings for a dashboard and start and stop the dashboard from within the Universal administrative interface.

## Adding a Dashboard

Dashboards can be added to Universal using the Add Dashboard button from the Dashboard / Dashboards page.

**Name**

Name is displayed throughout the UI and returned from the Universal cmdlets.

**Base URL**

The base URL is the URL that you will access to view this dashboard. This URL needs to be unique within this instance. You can specify the `/` root URL if you wish. You will have to visit `/admin` to login to the administrative page if you set the dashboard to the root URL.

**File Name**

The full file name to the dashboard file. This file needs to return a dashboard using New-UDDashboard.

**Environment**

The [environment ](../../config/environments.md)to run the dashboard within.

**Authentication**

Enables authentication for the dashboard.

**Roles**

Defines the role that is required to access the dashboard.

**AutoStart**

Determines whether the dashboard should start (or restart) when the server starts or changes are made to the dashboard files.

![](<../../.gitbook/assets/image (171).png>)

## Starting and Stopping Dashboards

Similar to jobs, dashboards run in separate PowerShell processes. You can start and stop a dashboard process by clicking the Start or Stop button from the Dashboards page.

## Viewing Diagnostic Information

You can view diagnostic information for a dashboard by clicking the Info button on the Dashboards page. This will show your start information for the dashboard as well as any error that were encountered when starting the dashboard.

## Viewing the Dashboard

You can view the dashboard by clicking the View button. This will take you to the Base URL for the dashboard.

## Executing Commands with the Dashboard

On the dashboard information page, click on the Console tab to view the UD console. The console allows you to run scripts from within the UD runspace so you can better debug the state of your script. You can evaluate variables and run commands that are available to the dashboard. You will be running in the context of your user in regards to the runspace but the process will be running as the service account user.

## Persistent Runspaces

Persistent runspaces allow you to maintain runspace state within your dashboard endpoints. This is important for users that perform some sort of initialization within their endpoints that they do not want to execute on subsequent calls.

By default, runspaces will be reset after each execution. This will cause variables, modules and functions defined during the execution of an endpoint.

To enable persistent runspaces, you will need to configure an [environment ](../../config/environments.md)for your API. Set the `-PersistentRunspace` parameter to enable this feature. This is configured in the `environments.ps1` script.

```
New-PSUEnvironment -Name 'Env' -Path 'powershell.exe' -PersistentRunspace
```

You will need to ensure that the environment is used by the dashboard.

## Automatically Granting App Tokens

You can automatically grant app tokens to users that visit dashboards. This is useful if you want to invoke the management API for PowerShell Universal from within a dashboard. Your dashboard will need to have authentication enabled and you will have to use the `-GrantAppToken` switch parameter on `New-PSUDashboard`.

```
New-PSUDashboard -Name 'Dashboard' -BaseUrl '/' -Framework "UniversalDashboard:Latest" -Authenticated -GrantAppToken
```

From within your dashboard, you can now invoke the management API without having to worry about app token management. The API will be invoked in the context of the user that is visiting the dashboard.

```
New-UDDashboard -Title "Hello, World!" -Content {
    New-UDButton -Text 'Job' -OnClick {
        Invoke-UAScript -Name 'Test.ps1'
    }
}
```

## Disable Error Toasts

By default, dashboards will display a toast message when an error is generated within an endpoint script. To avoid this behavior, you can use the `-DisableErrorToast` parameter of `New-UDDashboard`

```
New-PSUDashboard -Name 'Dashboard' -BaseUrl '/' -Framework "UniversalDashboard:Latest" -Authenticated -DisableErrorToast
```

```
New-UDDashboard -Title "Hello, World!" -Content {
    New-UDButton -Text 'Job' -OnClick {
        throw "Exception
    }
} 
```

## Disable Startup Logging

When starting a dashboard, information about the variables and modules is displayed within the dashboard log. If you wish to suppress this information, you can use the `-DisableStartupLogging` parameter.&#x20;

```
New-PSUDashboard -Name 'Dashboard' -BaseUrl '/' -Framework "UniversalDashboard:Latest" -DisableStartupLogging
```

## Variables Available in Dashboards

Built-in variables are listed on the [variables page.](../../platform/variables.md#dashboards)
