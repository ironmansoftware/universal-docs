# Variables

Variables allow for the global definition of variables that are available within scripts. You can also import secrets that are also available within scripts or as run as credentials.

{% hint style="info" %}
Variables are stored in the `variables.ps1` configuration file.
{% endhint %}

## Creating a Variable

To create a variable, navigate to the Platform \ Variables page. Click Add Variable to define a new variable.

Standard variables are just name \ value pairs of strings. They will be added to your scripts before they are run.

![](<../.gitbook/assets/image (451).png>)

## Creating a Secret Variable

Secret variables are stored within the selected vault. The value of those variables is never stored within Universal. To define a new secret variable, click Add Variable on the variables page and select the Secret tab.

From this dialog, you'll be able to define string and PSCredentials in the specified vault.

![](<../.gitbook/assets/image (277).png>)

### Credential Format

In some environments, it may be necessary to specify the domain name in the user name field. You can specify in either the `domain\user` or `user@domain` format. If you do not do so, you will receive errors when attempting to start processes, like scripts or dashboards, as that user account.

## Vaults

### Database

The database vault stores secrets within the PowerShell Universal database. These secrets are encrypted using AES encryption using a customizable key. You can customize the key by specifying the Secrets \ Database \ EncryptionKey.

#### appsettings.json

You can configure this setting in appsettings.json.

```json
"Secrets": {
  "Database": {
    "EncryptionKey": "=b0ywQA@VOSdr&R7an5g&XK6NVO%s4Tf"
  }
}
```

#### Environment Variable

You can configure this setting with an environment variable.

```powershell
$Env:Secrets__Database__EncryptionKey = "=b0ywQA@VOSdr&R7an5g&XK6NVO%s4Tf"
```

### BuiltInLocalVault

Values for secrets with the `BuiltInLocalVault` are stored within the Windows Credential Manager instance of the security principal that is running PSU. For example, the service account of the user running the Universal service. If you change users (such as running as a service account), the account will not have access to the previous user's secrets and you will need to add those secrets again.

### PSUSecretStore

The `PSUSecretStore` vault is integrated with the Microsoft `SecretStore` module to store secrets in a cross-platform file. Ths file is tied to the current user account running PowerShell Universal. The password for the vault is stored in `appsettings.json`.

### Az.KeyVault

By default, we do not include the Azure Key Vault extension directly in PowerShell Universal As of Powershell Universal v4.0.11, a container including the required Az.Accounts and Az.KeyVault modules is avilable to allow you use KeyVault out of the box. This can be found on [Docker Hub](https://hub.docker.com/r/ironmansoftware/universal/tags?page=1\&name=modules).

Below you will find how to configure it. This example uses an Azure hosted web-app version of PowerShell Universal.

In Azure, we'll need to configure a managed identity for our web app. This step isn't necessarily required if you are running outside of Azure. You can enable the managed identity under the Identity page for your web app.

![](<../.gitbook/assets/image (228).png>)

Next, you'll need to allow your managed identity to access your key vault and read your subscription. You can add the managed identity to the builtin Reader group to allow access to the subscription.

![](<../.gitbook/assets/image (430).png>)

Then, I provided all privileges to secret and key management for my managed identity in my Key Vault resource.

![](<../.gitbook/assets/image (457).png>)

Finally, we will need to register the key vault and connect to Azure when the web app starts. This can be accomplished by using the Az.Account and Az.KeyVault modules.

After deploying your web-app, you will need to first install the Az.Account and Az.KeyVault modules. You can do so on the modules page. They will be installed to the local repository within the web app.

![](<../.gitbook/assets/image (21).png>)

Next, create a script within PowerShell Universal to connect to Azure and register the vault. Run the script to verify it works properly.

```powershell
$sub = 'affdf0d4-eed5-48a6-889c-599d482xxxxx'
Connect-AzAccount -Id -Scope CurrentUser -SubscriptionId $sub

Register-SecretVault -ModuleName Az.KeyVault -Name AzureKeyVault -VaultParameters @{ 
    AZKVaultName = 'psu-demo'
    SubscriptionId = $sub
} -AllowClobber
```

Now, when you are creating secrets, you will see the AzureKeyVault available.

![](<../.gitbook/assets/image (310) (1) (1) (1).png>)

To ensure the application is connected to Azure and the key vault is registered, create a startup trigger to run the script when the web app starts. We recommend setting a delay when for the trigger to allow the app to warm up.

![](<../.gitbook/assets/image (45).png>)

## Importing Secret Variables

You can also import pre-existing secrets as variables into Universal. The variable values are not imported but will be looked up during execution. Click the Import Secret button to import secrets.

## Using Variables

Variables can be used in APIs, Scripts and Dashboards. When using the default environments, all variables are automatically imported. This is accomplished by specifying the `-Variable` parameter of `New-PSUEnvironment` with a wild card (\*). If you are using your own environments, you will have to configure [which variables you would like included](https://docs.powershelluniversal.com/config/environments#variables). You can reference a variable like you would any other PowerShell variable. The variable will contain the value you set. If you use a secret, it will contain the secret's value.

```
$MyVariable
```

You can customize which variables are allowed in an environment by customizing the environments `-Variable` parameter.

See [Environments](../config/environments.md#variables) for more information.

## Secret Scope

To access secrets that you have added to PowerShell Universal, you can use the `$Secret` scope. For example, if you defined a secret named `Credential`, you could access that secret anywhere with the secret scope. You cannot set secrets using the secret scope.

```powershell
Invoke-Command -Credential $Secret:Credential { Write-Host "Hello" }
```

### Access Variables by Name

You can access variables by name using the `$Secret:` prefix.

```powershell
# PSCredential
$Secret:MyNewSecret.UserName
$Secret:MyNewSecret.Password

# String
$Secret:DashboardSecret
```

### Access Values Dynamically

You can access the secret scope dynamically by using `Get-Item`. The secret scope is implemented as a provider. This is helpful if you don't have static variable names.

```powershell
# PSCredential
(Get-ChildItem "Secret:MyNewSecret").UserName
(Get-ChildItem "Secret:MyNewSecret").Password

# String
(Get-ChildItem "Secret:DashboardSecret")
```

### ForEach-Object -Parallel

In order to use secrets when using `ForEach-Object` with the `-Parallel` parameter, you will need to take advantage of the `$using` keyword.

```powershell
1..5 | ForEach-Object -Parallel {
  $using:Secret:MySecret
}
```

## Configuring the `PSUSecretStore` Password

By default, the `PSUSecretStore` vault password is stored within `appsettings.json` in Secrets \ SecretStore \ Password.

## Built-In Variables

The following variables are available throughout all environments within PowerShell Universal.

| Name            | Type   | Description                                                                |
| --------------- | ------ | -------------------------------------------------------------------------- |
| $PSUEnvironment | string | The name of the environment the script is running within (e.g. Integrated) |
| $Repository     | string | The absolute path to the repository folder.                                |

### API

There are a set of predefined variables that are available in API endpoints. You'll be able to use these variables in your scripts.

| Variable         | Description                                                                                                                                                                                                     | Type                                                     |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| $Url             | URL the client used to call the endpoint                                                                                                                                                                        | String                                                   |
| $Method          | The HTTP method used to call the endpoint                                                                                                                                                                       | String                                                   |
| $Headers         | Headers provided by the client to call the endpoint                                                                                                                                                             | Hashtable                                                |
| $Body            | The UTF8 encoded string of the content of the request                                                                                                                                                           | String                                                   |
| $Data            | Binary byte array for the content of the request                                                                                                                                                                | Byte\[]                                                  |
| $RemoteIpAddress | The remote IP address used to make the request.                                                                                                                                                                 | String                                                   |
| $LocalIpAddress  | The local IP address used to service the request.                                                                                                                                                               | String                                                   |
| $RemotePort      | The remote port that was called to make the request.                                                                                                                                                            | Integer                                                  |
| $LocalPort       | The local port that was used to service the request.                                                                                                                                                            | Integer                                                  |
| $Identity        | The identity name of the principal accessing the API.                                                                                                                                                           | String                                                   |
| $UrlDefinition   | The definition for the URL.                                                                                                                                                                                     | String                                                   |
| $ConnectionId    | The [HTTP Context connection ID](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.connectioninfo.id?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_ConnectionInfo\_Id).                  | String                                                   |
| $SessionId       | The [HTTP Context session ID.](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.isession.id?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_ISession\_Id)                                 | String                                                   |
| $RequestId       | The [HTTP Context request ID.](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.httpcontext.traceidentifier?view=aspnetcore-6.0#Microsoft\_AspNetCore\_Http\_HttpContext\_TraceIdentifier) | String                                                   |
| $ClaimsPrincipal | The claims principal of the current user. This is the same object that is provided to role-based access policies.                                                                                               | [ClaimPrincipal](../userinterfaces/role-based-access.md) |

### Apps

Below are variables that are available in apps in addition to the global variables.

| Name             | Description                                                                                                       | Type                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| $User            | The user name of the logged in user. $Null if authentication is disabled.                                         | String                                                   |
| $Roles           | The roles that the user has been granted. $Null if authentication is disabled.                                    | String\[]                                                |
| $RemoteIpAddress | The remote IP address of the connected user.                                                                      | String                                                   |
| $RemotePort      | The remote port of the connected user.                                                                            | Int                                                      |
| $ClaimsPrincipal | The claims principal of the current user. This is the same object that is provided to role-based access policies. | [ClaimPrincipal](../userinterfaces/role-based-access.md) |
| $Headers         | The headers provided by the browser.                                                                              | hashtable                                                |
| $Cookies         | The request cookies provided by the browser.                                                                      | hashtable                                                |
| $PSUAppToken     | The app token of the current user. Only available when -GrantAppToken is enabled.                                 | string                                                   |
| $PSUComputerName | The URL of the PSU server. Only available when -GrantAppToken is enabled.                                         | string                                                   |
| $DashboardName   | The name of the current app                                                                                       | string                                                   |
| $Query           | The query string parameters from the URL of the app                                                               | Hashtable                                                |
| $RefreshToken    | The refresh token when using OpenID Connect                                                                       | string                                                   |
| $AccessToken     | The app token when using OpenID Connect                                                                           | string                                                   |

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

* [New-PSUVariable](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUVariable.txt)
* [Get-PSUVariable](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Get-PSUVariable.txt)
* [Remove-PSUVariable](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Remove-PSUVariable.txt)
* [Set-PSUVariable](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Set-PSUVariable.txt)
