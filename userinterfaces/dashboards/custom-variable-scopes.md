# Custom Variable Scopes

## Custom Variable Scopes

Universal Dashboard exposes two custom variable scopes using custom providers. These providers allow you to store your variables in scopes that make sense for a web application. The cache scope is used to store variables that can be used within any endpoint inside a dashboard. The session scope is used to store variables that can be used for a single user's session of the dashboard.

### Cache Scope

Cache scope is used to store a variable that will be available in any endpoint. Cache scope is useful for storing data that may be shown in more than one control or may be time consuming to look up. This could be helpful for querying machine performance counters (e.g. Active Directory, Azure).

Just like any other scope, cache variables are defined with a prefix and a colon separator.

```powershell
$Cache:Computers = Get-ADComputer
```

Once assigned, the `$Cache:Computer` variable is available within any endpoint.

```powershell
New-UDMonitor -Title Computers -Endpoint {
    $Cache:Computers.Length | Out-UDMonitorData
}
```

### Page Scope&#x20;

Page scope stores variables in per browser tab or window. If a new tab is opened or the current one is closed, the state will be removed.

```powershell
New-UDForm -Content {
    New-UDTextbox -Id 'Name'
} -OnSubmit {
    $Page:Name = $EventData.Name
    Sync-UDElement -Id 'Name'
}

New-UDDynamic -Content {
    New-UDTypography $Page:Name
}
```

### Session Scope

Session scope is used to store a variable per session. A session is established when a user's browser first visit a dashboard. A cookie is stored in the user's browser that dictates that it is part of the session. Sessions have an idle timeout of 25 minutes.

Just like any other scope, cache variables are defined with a prefix and a colon separator.

```powershell
New-UDCheckbox -Label "Show chart" -OnChange {
   $Session:ShowChart = $EventData
}
```

Once assigned, the `$Session:ShowChart` variable is available in dashboard endpoints. Session variables are not available in REST API endpoints or scheduled endpoints.

```powershell
New-UDColumn -Endpoint {
    if ($Session:ShowChart) {
         New-UDChart ...
    }
}
```

Once a session is terminated, the session variables are cleared.
