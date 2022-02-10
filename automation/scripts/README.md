---
description: PowerShell scripts to execute within PowerShell Universal.
---

# Scripts

PowerShell scripts can be created within PowerShell Universal to execute manually, on a scheudle or when events happen within the platform. They are stored on disk and also persisted to a local or remote Git repository.

{% hint style="info" %}
Script properties are stored in the `scripts.ps1` configuration file.
{% endhint %}

## Add a New Script

To add a new script, you can click the New Script button within the Automation / Scripts page. There are various settings you can provide for the script.

![](<../../.gitbook/assets/image (307) (1) (1) (1).png>)

## Script Options

### **Name**

Name of the script as shown in Universal Automation. This will also be the name used to persist the script to disk. This setting needs to be unique within the current folder.

### **Description**

A description of the script. This is shown in various places within the UA UI and also returned by the Universal cmdlets.

### **Disable Manual Invocation**

Prevents a script from being run manually. This is enforced in the UI as well as the web server and cmdlets.

### **Manual Time**

This setting is used to track the amount of time saved.

### **Max Job History**

Defaults to 100. It defines the amount of jobs that are stored when running this script. Jobs are also cleaned up based on the server-wide job retention duration setting from within the Settings / General page.

### **Error Action**

Changes how the script reacts when there is an error within the script. By default, terminating and non-terminating errors are ignored and the script will always be successful. You can change this setting to stop to cause scripts to fail immediately when an error is encountered.

### **Environment**

Allows you to define the required PowerShell environment for the script. By default, it uses the server-wide default PowerShell environment. PowerShell environments are automatically located the first the Universal Server starts up or read from the `environments.ps1` file. You can also add Environment on the Settings / Environments page.

### **Timeout**

The number of minutes before the script will timeout. The default value of 0 means the script will run forever. Once a script reaches it's time out, it will be cancelled.

### Anonymous

The anonymous setting allows the script to be run when the user is not authenticated. This is useful when using scripts in Pages.

### Discard Pipeline

{% hint style="info" %}
Available in PowerShell Universal 2.8 or later.&#x20;
{% endhint %}

When checked, this will disable the storage of pipeline output. This will greatly reduce the CPU and storage overhead of jobs. The script will still write to the information, warning, and error streams.&#x20;

### **Concurrent Jobs**

Defines the maximum concurrent jobs the script can be run. Defaults to 100.

```powershell
New-PSUScript -Name Script.ps1 -Path Script.Ps1 -ConcurrentJobs 1
```

## Running a Script

You can run a script in the UI by click the Run button the Automation / Scripts page or by clicking View and then Run. In each case, you will be presented with the Run Dialog that allows you to select various settings for the job.

![](<../../.gitbook/assets/image (311) (1) (1) (1).png>)

### Running a Script With Parameters

{% hint style="info" %}
Learn more about [parameters here](parameters.md).
{% endhint %}

PowerShell Universal automatically determines the parameters as defined within your scripts. It takes advantage of static code analysis to determine the type, default values and some validation that is then presented within the UI.

For example, you may have a script with the following parameters.

```powershell
param(
    $Test,
    [DateTime]$Time, 
    [int]$Number,
    [PSCredential]$Credential,
    [System.ConsoleColor]$Color
)
```

The result is a set of input options that are based on the types of parameters.

![](<../../.gitbook/assets/image (312) (1) (1).png>)

### Running a Script as Another User

{% hint style="info" %}
The integrated [environment](../../config/environments.md) does not support running as alternate credentials.&#x20;
{% endhint %}

You can run scripts as another user by configuring [secret variables](../../platform/variables.md#creating-a-secret-variable). PowerShell Universal uses the Microsoft Secret Management module to integrate with secret providers. See variables for more information on secrets.

To run as another user, simply add or import a PSCredential variable. From there, you can select the credential from within the run dialog.

![](<../../.gitbook/assets/image (301).png>)

## Remoting

Note that you can use PowerShell remoting by taking advantage of `Invoke-Command` . We do not support the use of `Enter-PSSession` or `Import-PSSession`.

## Comment-Based Help

{% hint style="info" %}
This feature is available in PowerShell Universal 2.5 or later.
{% endhint %}

You can use comment-based to define the description, a synopsis, parameter based help, and links for your scripts. These will be displayed within the PowerShell Universal UI.&#x20;

```powershell
<#
.SYNOPSIS 

This is a script for pinging other computers. 

.DESCRIPTION

This script can ping other computers. 

.PARAMETER HostName

The host name or address to ping. 

.LINK
https://www.ironmansoftware.com
#>
param($HostName)

Test-NetConnection $HostName
```

This above will yield the following user interface. The synopsis will be shown as the short description and a longer description can be shown in the description section. Links will appear under the description.&#x20;

![](<../../.gitbook/assets/image (306) (1) (1) (1) (1).png>)



## API

* [New-PSUScript](../../cmdlets/New-PSUScript.txt)
* [Remove-PSUScript](../../cmdlets/Remove-PSUScript.txt)
* [Set-PSUScript](../../cmdlets/Set-PSUScript.txt)
* [Get-PSUScript](../../cmdlets/Get-PSUScript.txt)

