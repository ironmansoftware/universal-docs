---
description: Performance profiler for PowerShell Universal.
---

# Profiling

{% hint style="info" %}
Profiling only works for the integrated environment.
{% endhint %}

PowerShell Universal provides a performance profiler for debugging issues where the platform may exhibit slow responses. This is primarily useful when building Dashboards.&#x20;

## Enable Profiling

Profiling will increase memory usage as profiling data is stored in memory. You can enable profiling by configuring the `Profiling` appsettings.json property. It is `false` by default. You will need to restart PowerShell Universal after enabling or disabling profiling.&#x20;

```json
"Profiling": true
```

## Access Profiling Data

You can access profiling data by navigating to `/profiler/results-index` . You will need to be logged in as administrator before being able to access this URL.&#x20;

You will see a list of requests and their timings.&#x20;

![Result Index](<../.gitbook/assets/image (432).png>)

Clicking on the request will display a break-down of the timings.&#x20;

![Timings](<../.gitbook/assets/image (266).png>)

## Profiling an API Endpoint

You can profile an API endpoint using `Measure-PSUBlock`. The API will be listed by URL in the result index.&#x20;

For example, assume an API called `/process`.&#x20;

```powershell
New-PSUEndpoint -Url "/process" -Endpoint {
    Measure-PSUBlock -Name 'Api' -ScriptBlock {
        Get-Process | Select-Object name
    }
} -Authentication -Timeout 0 
```

The result of profiling this API would be listed by URL.

![](<../.gitbook/assets/image (440).png>)

Viewing the profile for this API would list the block we measured.&#x20;

![](<../.gitbook/assets/image (556).png>)

## Profiling an App

{% hint style="info" %}
`Measure-UDBlock` is an alias for `Measure-PSUBlock`
{% endhint %}

You can use the built-in profiler with Apps. By default, certain internal action timings are recorded. You can also use the `Measure-PSUBlock` cmdlet to measure specific blocks within your dashboard.&#x20;

For example, this app uses `Measure-PSUBlock` to measure the performance of the `Start-Sleep` cmdlet. The result is the block will take one second to execute.&#x20;

```powershell
New-UDApp -Title 'App' -Content {
    New-UDDynamic -Id 'MyElement' -Content {
        Measure-PSUBlock -Name 'WithinDashboard' -ScriptBlock {
            Start-Sleep 1
        }
    }
}
```

When reviewing requests within the profiler, you will want to look for `UDComponent\ElementPost` and `UDComponent\Element`. These are requests for elements within Apps.&#x20;

Below is the example output from the app shown above. Notice that the URL includes the element's ID `MyElement`. You'll also notice that the `WithinDashboard` block takes about 1 second.&#x20;

![Dashboard Timing](<../.gitbook/assets/image (264).png>)

Not all timing will be displayed by default. You can click `show trivial` to expand all timings.&#x20;

![All Timings](<../.gitbook/assets/image (549).png>)

## Profiling a Job

You can profile jobs by using `Measure-PSUBlock` within your script.&#x20;

For example, assume we have a script that calls `Get-Service`.&#x20;

```powershell
Measure-PSUBlock -ScriptBlock {
    Get-Service
} -Name 'Get-Service'
```

Running a profile on this script will list the job as `JobProfiler/{id}`. The id will match the job ID shown in the admin console.&#x20;

![](<../.gitbook/assets/image (554).png>)

The profile will include the block that was measured.&#x20;

![](<../.gitbook/assets/image (111).png>)
