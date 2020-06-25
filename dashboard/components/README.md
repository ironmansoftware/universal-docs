# Components

Components are pluggable widgets that can be added to Universal Dashboard. There are two components that are built in to PSU. These include the Nivo charts library as well as the UDMap component. Additional components can be downloaded from the [UD Marketplace](https://marketplace.universaldashboard.io/).

When building a dashboard, you can simply call the PowerShell cmdlets within your dashboard script to create a new component.

```text
New-UDDashboard -Title 'Dashboard' -Content {
    New-UDTypography -Text 'Hello, world!'
}
```

