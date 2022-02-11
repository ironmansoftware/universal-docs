---
description: Performance profiler for PowerShell Universal.
---

# Profiling

{% hint style="info" %}
Available in PowerShell Universal 2.8.2 or later
{% endhint %}

PowerShell Universal provides a performance profiler for debugging issues where the platform may exhibit slow responses. This is primarily useful when building Dashboards.&#x20;

## Access Profiling Data

You can access profiling data by navigating to `/profiler/results-index` . You will need to be logged in as administrator before being able to access this URL.&#x20;

You will see a list of requests and their timings.&#x20;

![Result Index](<../.gitbook/assets/image (319).png>)

Clicking on the request will display a break-down of the timings.&#x20;

![Timings](<../.gitbook/assets/image (309).png>)

## Profiling a Dashboard

{% hint style="info" %}
Profiling only works with the Integrated environment.&#x20;
{% endhint %}

You can use the built-in profiler with Dashboards. By default, certain internal action timings are recorded. You can also use the `Measure-PSUBlock` cmdlet to measure specific blocks within your dashboard.&#x20;

For example, this dashboard uses `Measure-PSUBlock` to measure the performance of the `Start-Sleep` cmdlet. The result is the block will take one second to execute.&#x20;

```powershell
New-UDDashboard -Title 'Dashboard' -Content {
    New-UDDynamic -Id 'MyElement' -Content {
        Measure-PSUBlock -Name 'WithinDashboard' -ScriptBlock {
            Start-Sleep 1
        }
    }
}
```

When reviewing requests within the profiler, you will want to look for `UDComponent\ElementPost` and `UDComponent\Element`. These are requests for elements within Dashboards.&#x20;

Below is the example output from the dashboard shown above. Notice that the URL includes the element's ID `MyElement`. You'll also notice that the `WithinDashboard` block takes about 1 second.&#x20;

![Dashboard Timing](<../.gitbook/assets/image (300).png>)

Not all timing will be displayed by default. You can click `show trivial` to expand all timings.&#x20;

![All Timings](<../.gitbook/assets/image (308).png>)
