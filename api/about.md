# About

Universal provides the ability to define REST API endpoints using PowerShell. When the endpoints are executed by a compatible HTTP client, the PowerShell script will execute and return the result to the end user.

{% hint style="info" %}
This feature is for developing custom APIs run by Universal. It not required for managing Universal. Universal provides a set of management APIs that are included with the platform.
{% endhint %}

{% embed url="https://youtu.be/M6z0iYhmUkQ" caption="" %}

## Execution Environment

The REST API execution environment runs in your default PowerShell version. Unlike Automation jobs, which can also be run via the Universal management API, APIs that you define are run in a single PowerShell process. Because the PowerShell process is not started and stopped for each call to the endpoint, the API is much faster.

You can define the [environment ](../config/environments.md)that runs the PowerShell Universal API process by specifying the `-ApiEnvironment` on `Set-PSUSetting`. Changing this setting will cause the API process to restart. 

```PowerShell
Set-PSUSetting -ApiEnvironment '7.1'
```

### Performance

Performance is relative to the hardware and network conditions that you are running Universal on. That said, in ideal conditions you can expect the Universal APIs to service about 500 requests per second. This is with an entirely empty endpoint so any script that you add to that endpoint will reduce the throughput. The reduction of throughput will depend on the cmdlets and script executed within the API endpoint.

### Variables

There are a set of predefined variables that are available in API endpoints. You'll be able to use these variables in your scripts.

| Variable | Description | Type |
| :--- | :--- | :--- |
| $Url | URL the client used to call the endpoint | String |
| $Headers | Headers provided by the client to call the endpoint | Hashtable |
| $Body | The UTF8 encoded string of the content of the request | String |
| $Data | Binary byte array for the content of the request | Byte\[\] |
| $RemoteIpAddress | The remote IP address used to make the request. | String |
| $LocalIpAddress | The local IP address used to service the request. | String |
| $RemotePort | The remote port that was called to make the request. | Integer |
| $LocalPort | The local port that was used to service the request. | Integer |
| $Identity | The identity name of the principal accessing the API. | String |

## Related Cmdlets

* [New-PSUEndpoint](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/New-PSUEndpoint.md)
* [Get-PSUEndpoint](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Get-PSUEndpoint.md)
* [Remove-PSUEndpoint](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Remove-PSUEndpoint.md)
* [New-PSUApiResponse](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/New-PSUApiResponse.md)
* [Set-UASetting](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Set-UASetting.md)

