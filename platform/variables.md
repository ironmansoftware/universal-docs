# Variables

Variables allow for the global definition of variables that are available within scripts. You can also import secrets that are also available within scripts or as run as credentials.&#x20;

{% hint style="info" %}
Variables are stored in the `variables.ps1` configuration file.
{% endhint %}

## Creating a Variable&#x20;

To create a variable, navigate to the Automation / Variables page. Click Add Variable to define a new variable.&#x20;

Standard variables are just name \ value pairs of strings. They will be added to your scripts before they are run.&#x20;

!['](<../.gitbook/assets/image (14).png>)

## Creating a Secret Variable

{% hint style="warning" %}
Secret management is currently only supported on Windows.&#x20;
{% endhint %}

Secret variables are stored within the selected vault. The value of those variables are never stored within Universal. To define a new secret variable, click Add Variable on the variables page and select the Secret tab.&#x20;

{% hint style="warning" %}
Values for secrets are stored within the current user's Windows Credential Manager instance. If you change users (such as running as a service account), the account will not have access to the previous user's secrets and you will need to add those secrets again.
{% endhint %}

From this dialog, you'll be able to define string and PSCredentials in the specified vault.&#x20;

![](<../.gitbook/assets/image (11).png>)

## Importing Secret Variables

You can also import pre-existing secrets as variables into Universal. The variable values are not imported but will be looked up during execution. Click the Import Secret button to import secrets.&#x20;

## Using Variables

Variables can be used in APIs, Scripts and Dashboards. When using the default environments, all variables are automatically imported. This is accomplished by specifying the `-Variable` parameter of `New-PSUEnvironment` with a wild card (\*). If you are using your own environments, you will have to configure [which variables you would like included](https://docs.powershelluniversal.com/config/environments#variables). You can reference a variable like you would any other PowerShell variable. The variable will contain the value you set. If you use a secret, it will contain the secret's value. &#x20;

```
$MyVariable
```

You can customize which variables are allowed in an environment by customizing the environments `-Variable` parameter.&#x20;

See [Environments](../config/environments.md#variables) for more information.&#x20;

## Performance of Secrets

PowerShell Universal uses the Microsoft Secret Management module. The built-in vault uses the Windows Credential Manager to store secrets. Due to the implementation of the `Get-Secret` cmdlet, it may cause performance issues when you have many secrets.&#x20;

You may want to consider limiting the number of secrets that you include in each environment to improve performance.

## Built-In Variables

The following variables are available throughout all environments within PowerShell Universal.&#x20;

| Name            | Type   | Description                                                                |
| --------------- | ------ | -------------------------------------------------------------------------- |
| $PSUEnvironment | string | The name of the environment the script is running within (e.g. Integrated) |

### API

There are a set of predefined variables that are available in API endpoints. You'll be able to use these variables in your scripts.

| Variable         | Description                                                                                                                                                                                                     | Type      |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| $Url             | URL the client used to call the endpoint                                                                                                                                                                        | String    |
| $Headers         | Headers provided by the client to call the endpoint                                                                                                                                                             | Hashtable |
| $Body            | The UTF8 encoded string of the content of the request                                                                                                                                                           | String    |
| $Data            | Binary byte array for the content of the request                                                                                                                                                                | Byte\[]   |
| $RemoteIpAddress | The remote IP address used to make the request.                                                                                                                                                                 | String    |
| $LocalIpAddress  | The local IP address used to service the request.                                                                                                                                                               | String    |
| $RemotePort      | The remote port that was called to make the request.                                                                                                                                                            | Integer   |
| $LocalPort       | The local port that was used to service the request.                                                                                                                                                            | Integer   |
| $Identity        | The identity name of the principal accessing the API.                                                                                                                                                           | String    |
| $UrlDefinition   | The definition for the URL.                                                                                                                                                                                     | String    |
| $ConnectionId    | The [HTTP Context connection ID](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.connectioninfo.id?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_ConnectionInfo\_Id).                  | String    |
| $SessionId       | The [HTTP Context session ID.](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.isession.id?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_ISession\_Id)                                 | String    |
| $RequestId       | The [HTTP Context request ID.](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httpcontext.traceidentifier?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_HttpContext\_TraceIdentifier) | String    |

### Dashboards

Below are variables that are available in dashboards in addition to the global variables.

| Name             | Description                                                                                                       | Type                                                                |
| ---------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| $User            | The user name of the logged in user. $Null if authentication is disabled.                                         | String                                                              |
| $Roles           | The roles that the user has been granted. $Null if authentication is disabled.                                    | String\[]                                                           |
| $RemoteIpAddress | The remote IP address of the connected user.                                                                      | String                                                              |
| $RemotePort      | The remote port of the connected user.                                                                            | Int                                                                 |
| $ClaimsPrincipal | The claims principal of the current user. This is the same object that is provided to role-based access policies. | [ClaimPrincipal](../userinterfaces/dashboards/role-based-access.md) |
| $Headers         | The headers provided by the browser.                                                                              | hashtable                                                           |
| $Cookies         | The request cookies provided by the browser.                                                                      | hashtable                                                           |
| $PSUAppToken     | The app token of the current user. Only available when -GrantAppToken is enabled.                                 | string                                                              |
| $PSUComputerName | The URL of the PSU server. Only available when -GrantAppToken is enabled.                                         | string                                                              |

### Scripts

There are several built-in variables that are defined when a job is run. You can use these variables in your scripts to retrieve information about the current job.

| Name          | Description                                                                                                                                   |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| $UAJob        | The current job that is running. This will include properties such as the script, the user that started the job and when the job was started. |
| $UAJobId      | The ID of the running job.                                                                                                                    |
| $UAScript     | The script that is running. This will include properties such as the name of the script and path to the script.                               |
| $UAScriptId   | The ID of the running script.                                                                                                                 |
| $UASchedule   | The schedule that was used to start the script.                                                                                               |
| $UAScheduleId | The ID of the schedule that started the script.                                                                                               |
| $AccessToken  | When using OIDC authentication, you can retrieve the current user's access token for access resources on their behalf.                        |

#### Retrieving the user that started a script

You can retrieve the name of the user that started the script by using the `UAJob` variable

```
$UAJob.Identity.Name
```

## Related Cmdlets

* [New-UAVariable](../cmdlets/Universal/New-UAVariable.md)
* [Get-UAVariable](../cmdlets/Universal/Get-UAVariable.md)
* [Remove-UAVariable](../cmdlets/Universal/Remove-UAVariable.md)
* [Set-UAVariable](../cmdlets/Universal/Set-UAVariable.md)

