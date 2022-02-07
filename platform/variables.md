# Variables

Variables allow for the global definition of variables that are available within scripts. You can also import secrets that are also available within scripts or as run as credentials.

{% hint style="info" %}
Variables are stored in the `variables.ps1` configuration file.
{% endhint %}

## Creating a Variable

To create a variable, navigate to the Automation / Variables page. Click Add Variable to define a new variable.

Standard variables are just name \ value pairs of strings. They will be added to your scripts before they are run.

!['](<../.gitbook/assets/image (14).png>)

## Creating a Secret Variable

Secret variables are stored within the selected vault. The value of those variables are never stored within Universal. To define a new secret variable, click Add Variable on the variables page and select the Secret tab.

From this dialog, you'll be able to define string and PSCredentials in the specified vault.

![](<../.gitbook/assets/image (11).png>)

## Vaults

### BuiltInLocalVault

Values for secrets with the `BuiltInLocalVault` are stored within the Windows Credential Manager instance of the security principal that is running PSU. For example, the service account of the user running the Universal service. If you change users (such as running as a service account), the account will not have access to the previous user's secrets and you will need to add those secrets again.

### PSUSecretStore

{% hint style="info" %}
PowerShell Universal 2.6 or later.
{% endhint %}

The `PSUSecretStore` vault is integrated with the Microsoft `SecretStore` module to store secrets in a cross-platform file. Ths file is tied to the current user account running PowerShell Universal. The password for the vault is stored in `appsettings.json`.

### Az.KeyVault

{% hint style="info" %}
Requires PowerShell Universal 2.7 or later.
{% endhint %}

We do not include the Azure Key Vault extension directly in PowerShell Universal, but below you will find how to configure it. This example uses an Azure hosted web-app version of PowerShell Universal.&#x20;

In Azure, we'll need to configure a managed identity for our web app. This step isn't necessarily required if you are running outside of Azure. You can enable the managed identity under the Identity page for your web app.&#x20;

![](<../.gitbook/assets/image (303) (1).png>)

Next, you'll need to allow your managed identity to access your key vault and read your subscription. You can add the managed identity to the builtin Reader group to allow access to the subscription.

![](<../.gitbook/assets/image (302) (1).png>)

Then, I provided all privileges to secret and key management for my managed identity in my Key Vault resource.

![](<../.gitbook/assets/image (307) (1) (1).png>)

Finally, we will need to register the key vault and connect to Azure when the web app starts. This can be accomplished by using the Az.Account and Az.KeyVault modules.&#x20;

After deploying your web-app, you will need to first install the Az.Account and Az.KeyVault modules. You can do so on the modules page. They will be installed to the local repository within the web app.

![](<../.gitbook/assets/image (305) (1) (1).png>)

Next, create a script within PowerShell Universal to connect to Azure and register the vault. Run the script to verify it works properly.

```powershell
$sub = 'affdf0d4-eed5-48a6-889c-599d482xxxxx'
Connect-AzAccount -Id -Scope CurrentUser -SubscriptionId $sub

Register-SecretVault -ModuleName Az.KeyVault -Name AzureKeyVault -VaultParameters @{ 
    AZKVaultName = 'psu-demo'
    SubscriptionId = $sub
} -AllowClobber
```

Now, when you are creating secrets, you will see the AzureKeyVault available.&#x20;

![](<../.gitbook/assets/image (310) (1) (1).png>)

To ensure the application is connected to Azure and the key vault is registered, create a startup trigger to run the script when the web app starts. We recommend setting a delay when for the trigger to allow the app to warm up.&#x20;

![](<../.gitbook/assets/image (304) (1) (1).png>)

## Importing Secret Variables

You can also import pre-existing secrets as variables into Universal. The variable values are not imported but will be looked up during execution. Click the Import Secret button to import secrets.

## Using Variables

Variables can be used in APIs, Scripts and Dashboards. When using the default environments, all variables are automatically imported. This is accomplished by specifying the `-Variable` parameter of `New-PSUEnvironment` with a wild card (\*). If you are using your own environments, you will have to configure [which variables you would like included](https://docs.powershelluniversal.com/config/environments#variables). You can reference a variable like you would any other PowerShell variable. The variable will contain the value you set. If you use a secret, it will contain the secret's value.

```
$MyVariable
```

You can customize which variables are allowed in an environment by customizing the environments `-Variable` parameter.

See [Environments](../config/environments.md#variables) for more information.

## Performance of Secrets

PowerShell Universal uses the Microsoft Secret Management module. The built-in vault uses the Windows Credential Manager to store secrets. Due to the implementation of the `Get-Secret` cmdlet, it may cause performance issues when you have many secrets.

You may want to consider limiting the number of secrets that you include in each environment to improve performance.

## Configuring the `PSUSecretStore` Password

{% hint style="info" %}
PowerShell Universal 2.6 or later.
{% endhint %}

By default, the `PSUSecretStore` vault password is stored within `appsettings.json` in Secrets \ SecretStore \ Password.

## Built-In Variables

The following variables are available throughout all environments within PowerShell Universal.

| Name            | Type   | Description                                                                |
| --------------- | ------ | -------------------------------------------------------------------------- |
| $PSUEnvironment | string | The name of the environment the script is running within (e.g. Integrated) |
| $Repository     | string | The absolute path to the repository folder.                                |

### API

There are a set of predefined variables that are available in API endpoints. You'll be able to use these variables in your scripts.

| Variable         | Description                                                                                                                                                                                                     | Type                                                                |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| $Url             | URL the client used to call the endpoint                                                                                                                                                                        | String                                                              |
| $Headers         | Headers provided by the client to call the endpoint                                                                                                                                                             | Hashtable                                                           |
| $Body            | The UTF8 encoded string of the content of the request                                                                                                                                                           | String                                                              |
| $Data            | Binary byte array for the content of the request                                                                                                                                                                | Byte\[]                                                             |
| $RemoteIpAddress | The remote IP address used to make the request.                                                                                                                                                                 | String                                                              |
| $LocalIpAddress  | The local IP address used to service the request.                                                                                                                                                               | String                                                              |
| $RemotePort      | The remote port that was called to make the request.                                                                                                                                                            | Integer                                                             |
| $LocalPort       | The local port that was used to service the request.                                                                                                                                                            | Integer                                                             |
| $Identity        | The identity name of the principal accessing the API.                                                                                                                                                           | String                                                              |
| $UrlDefinition   | The definition for the URL.                                                                                                                                                                                     | String                                                              |
| $ConnectionId    | The [HTTP Context connection ID](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.connectioninfo.id?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_ConnectionInfo\_Id).                  | String                                                              |
| $SessionId       | The [HTTP Context session ID.](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.isession.id?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_ISession\_Id)                                 | String                                                              |
| $RequestId       | The [HTTP Context request ID.](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httpcontext.traceidentifier?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_HttpContext\_TraceIdentifier) | String                                                              |
| $ClaimsPrincipal | The claims principal of the current user. This is the same object that is provided to role-based access policies.                                                                                               | [ClaimPrincipal](../userinterfaces/dashboards/role-based-access.md) |

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

## API

* [New-PSUVariable](../cmdlets/New-PSUVariable.txt)
* [Get-PSUVariable](../cmdlets/Get-PSUVariable.txt)
* [Remove-PSUVariable](../cmdlets/Remove-PSUVariable.txt)
* [Set-PSUVariable](../cmdlets/Set-PSUVariable.txt)
