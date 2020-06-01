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

