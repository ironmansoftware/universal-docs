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
|                 |        |                                                                            |
|                 |        |                                                                            |

## Related Cmdlets

* [New-UAVariable](../cmdlets/Universal/New-UAVariable.md)
* [Get-UAVariable](../cmdlets/Universal/Get-UAVariable.md)
* [Remove-UAVariable](../cmdlets/Universal/Remove-UAVariable.md)
* [Set-UAVariable](../cmdlets/Universal/Set-UAVariable.md)

