# Migrating From Universal Dashboard 2.9

PowerShell Universal Dashboard v2.9 is a PowerShell module that allows you to create dashboard with PowerShell script. It is the predecessor to PowerShell Universal. The technology the enabled UD has been migrated into PowerShell Universal. You should be able to run the same PowerShell scripts in PowerShell Universal that you would in Universal Dashboard with some minor modifications.

### No need to call Start-UDDashboard

In Universal, all you need to do is return the result of New-UDDashboard from your script. There is no need to call Start-UDDashboard. The configuration of the webserver is taken place using the PSU `appsetting.json` file. 

```text
New-UDDashboard -Title 'My dashboard' -Content {

}
```

### Scheduled Endpoints

You do not need to pass the value of a scheduled endpoint to anything. You can just call `New-UDEndpoint` with a endpoint schedule and it will automatically be registed with PSU. 

```text
$EndpointSchedule = New-UDEndpointSchedule -Every 10 -Minute
$Endpoint = New-UDEndpoint -Schedule $Schedule -Endpoint {} 
```

### REST APIs 

REST APIs will be a separate feature of PSU and not a part of UD. 

### Authentication and Authorization

Authentication and authorization are now handled by PSU and there is no need to configure UD login pages. Authentication and authorization are configured with the PSU `appsettings.json` file. Dashboard's themselves can be either authenticated or not authenticated. A license is required to enable authenticated dashboards. 

To enable role-based access controls, you can assign roles to pages and use the automatic `$Roles` variable to check which roles the user is a part of. The `$User` variable will provide the name of the user. 

### Published Folders 

Published folders are not yet a feature of PSU. They will be implemented at a later time. 

## Migrating to Universal Dashboard v3

As we more closer to completion of Universal Dashboard v3 this section will become more complete. We'd like to start documenting this so that users can begin working with UDv3. 

### New-UDTable \(formerly UDGrid and UDTable\)

Rather than having two cmdlets for tables \(New-UDTable and New-UDGrid\). The New-UDTable in v3 provides the ability to display data in a table, filter, page, and sort it. It supports both client and server-side processing. 

You can view examples of the [table on GitHub](https://github.com/ironmansoftware/universal-dashboard/blob/master/src/v3/example/pages/data-display/table.ps1).

### New-UDDynamic

Unlink in v3, components do not have `-Endpoint` and `-Content` parameters. Each component will instead simply have a `-Content` parameter. To achieve dynamic sections of a page, you can instead use the `New-UDDynamic` cmdlet. This cmdlets let you define an entire section of a page as dynamic. It also provides auto refresh functionality so you can refresh sections of a page all at once. 

```text
New-UDDynamic -Endpoint {
    New-UDTypography -Text (Get-Date)
}
```

### New-UDGrid 

New-UDGrid allows you to define a grid layout using the Material UI library. You use this single cmdlet to define rows and columns within your dashboard. 

You can view examples of the [grid on GitHub](https://github.com/ironmansoftware/universal-dashboard/blob/master/src/v3/example/pages/layout/grid.ps1).

### New-UDForm \(formerly UDInput\)

`New-UDInput` has been replaced by `New-UDForm`. The UDForm component allows far more configuration that UDInput did. You will use the standard controls like UDTextbox, UDCheckbox, and UDSelect instead of New-UDInputField. This means that there are a single set of input cmdlets to use for UD. 

All of the input control examples can be [found on GitHub](https://github.com/ironmansoftware/universal-dashboard/tree/master/src/v3/example/pages/inputs).

### Navigation 

Instead of using New-UDSideNav, you will now use a combination of New-UDAppbar and New-UDDrawer. When New-UDAppBar is used with the default position, it will overlay the AppBar at the top of the page. You can then specify a drawer to customize the navigation experience within your dashboard. 

You can see examples of how to do [navigation on GitHub](https://github.com/ironmansoftware/universal-dashboard/blob/master/src/v3/example/pages/surfaces/appbar.ps1).

### Nivo and Sparklines are now open source

The Nivo and sparklines controls are now open source and on the Universal Dashboard repository. You can now use them without purchasing a license. 

For more examples of Nivo and sparklines controls, [see GitHub](https://github.com/ironmansoftware/universal-dashboard/tree/master/src/v3/example/pages/charts).

### Map is now open source

The map control is also open source and on GitHub. 

You can find examples [on GitHub](https://github.com/ironmansoftware/universal-dashboard/blob/master/src/v3/example/pages/data-display/map.ps1).

