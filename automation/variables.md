# Variables

Variables allow for the global definition of variables that are available within scripts. You can also import secrets that are also available within scripts or as run as credentials. 

{% hint style="info" %}
Variables are stored in the `variables.ps1` configuration file.
{% endhint %}

## Creating a Variable 

To create a variable, navigate to the Automation / Variables page. Click Add Variable to define a new variable. 

Standard variables are just name \ value pairs of strings. They will be added to your scripts before they are run. 

![&apos;](../.gitbook/assets/image%20%2814%29.png)

## Creating a Secret Variable

{% hint style="warning" %}
Secret management is currently only supported on Windows. 
{% endhint %}

Secret variables are stored within the selected vault. The value of those variables are never stored within Universal. To define a new secret variable, click Add Variable on the variables page and select the Secret tab. 

{% hint style="warning" %}
Values for secrets are stored within the current user's Windows Credential Manager instance. If you change users \(such as running as a service account\), the account will not have access to the previous user's secrets and you will need to add those secrets again.
{% endhint %}

From this dialog, you'll be able to define string and PSCredentials in the specified vault. 

![](../.gitbook/assets/image%20%2811%29.png)

## Importing Secret Variables

You can also import pre-existing secrets as variables into Universal. The variable values are not imported but will be looked up during execution. Click the Import Secret button to import secrets. 

## Related Cmdlets

* [New-UAVariable](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/New-UAVariable.md)
* [Get-UAVariable](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Get-UAVariable.md)
* [Remove-UAVariable](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Remove-UAVariable.md)
* [Set-UAVariable](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Universal/Set-UAVariable.md)



