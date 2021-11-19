# About

Universal provides the ability to define REST API endpoints using PowerShell. When the endpoints are executed by a compatible HTTP client, the PowerShell script will execute and return the result to the end user.

{% hint style="info" %}
This feature is for developing custom APIs run by Universal. It not required for managing Universal. Universal provides a set of management APIs that are included with the platform.
{% endhint %}

{% embed url="https://youtu.be/M6z0iYhmUkQ" %}

## Execution Environment

The REST API execution environment runs in your default PowerShell version. Unlike Automation jobs, which can also be run via the Universal management API, APIs that you define are run in a single PowerShell process. Because the PowerShell process is not started and stopped for each call to the endpoint, the API is much faster.

You can define the [environment ](../config/environments.md)that runs the PowerShell Universal API process by specifying the `-ApiEnvironment` on `Set-PSUSetting`. Changing this setting will cause the API process to restart.

```
Set-PSUSetting -ApiEnvironment '7.1'
```

### Performance

Performance is relative to the hardware and network conditions that you are running Universal on. That said, in ideal conditions you can expect the Universal APIs to service about 500 requests per second. This is with an entirely empty endpoint so any script that you add to that endpoint will reduce the throughput. The reduction of throughput will depend on the cmdlets and script executed within the API endpoint.

### Variables

Variables are listed on the [variables page](../platform/variables.md#api).

## Related Cmdlets

* [New-PSUEndpoint](../cmdlets/Universal/New-PSUEndpoint.md)
* [Get-PSUEndpoint](../cmdlets/Universal/Get-PSUEndpoint.md)
* [Remove-PSUEndpoint](../cmdlets/Universal/Remove-PSUEndpoint.md)
* [New-PSUApiResponse](../cmdlets/Universal/New-PSUApiResponse.md)
* [Set-UASetting](../cmdlets/Universal/Set-UASetting.md)
