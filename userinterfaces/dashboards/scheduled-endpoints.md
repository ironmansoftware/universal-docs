---
description: Simple scheduled endpoints within dashboards.
---

# Scheduled Endpoints

{% hint style="info" %}
We recommend you consider [Scheduled jobs](../../automation/schedules.md) over scheduled endpoints for jobs that require tracking of output, input, history or complex scheduling rules.
{% endhint %}

Scheduled endpoints allow you to run PowerShell script blocks on a schedule within your dashboards. Scheduled endpoints are more light weight than scheduled jobs but do not provide the same level of functionality. They do not track any history, the output is not logged and the schedules are not visible within the UI.

Scheduled endpoints are useful when loading and caching data that you will only use in your dashboard. Data stored within the dashboard cache is not shared across PowerShell Universal.

## Scheduling an Endpoint

The below is an example of scheduling an endpoint that runs every 10 seconds and stores information in a cache variable. This type of configuration increases performance of the dashboard for end users since the cache data is returned rather than calling Get-Process with each load of the dashboard.

```powershell
$EndpointSchedule = New-UDEndpointSchedule -Every 10 -Second
New-UDEndpoint -Schedule $EndpointSchedule -Endpoint {
    $Cache:Processes = Get-Process | Select-Object Name,ID
} | Out-Null

New-UDDashboard -Tiele 'Test' -Content {
    New-UDTable -Data $Cache:Processes
}
```

### Caching Server-Wide Data

You can also use the[ server-wide data ](../../platform/cache.md)caching features in dashboards. This means that you will be able to access that data throughout PowerShell Universal scripts. In your dashboard, you can load the cache with the scheduled endpoint.

```powershell
$EndpointSchedule = New-UDEndpointSchedule -Every 10 -Second
New-UDEndpoint -Schedule $EndpointSchedule -Endpoint {
   $Processes = Get-Process | Select-Object Name,ID
   Set-PSUCache -Name 'Processes' -Value $Processes
} | Out-Null

New-UDDashboard -Title 'Test' -Content {

}
```

You can then use the cache data in your API.

```powershell
New-PSUEndpoint -Url '/process' -Method Get -Endpoint {
    Get-PSUCache -Name 'Processes'
}
```

## API

* [New-UDEndpoint](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDEndpoint.txt)
* [New-UDEndpointSchedule](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDEndpointSchedule.txt)
