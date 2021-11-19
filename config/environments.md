---
description: Information about execution environments.
---

# Environments

Environments allow you to define an executable, arguments, modules and variables to use when running scripts, hosting APIs and dashboards.&#x20;

Environments are stored within the `environments.ps1` file.&#x20;

## Configuring Environments

To configure environments, you can use the Settings \ Environments page.&#x20;

![](<../.gitbook/assets/image (136).png>)

Environments support setting the name, path, arguments, modules and variables.

![](<../.gitbook/assets/image (135).png>)

### Name&#x20;

The name of the environment. This name will be shown through out the rest of the platform when running scripts, configuring the API host environment and hosting dashboards.&#x20;

### Path and Arguments

Environments support defining a path to an executable and arguments for that executable. These should be either PowerShell.exe or Pwsh.exe.&#x20;

You can also define modules and variables.&#x20;

### Modules

The modules list allows you to define zero or more modules to load in the PowerShell runspaces for the environment. These modules will be part of the initial session state so they will not need to be loaded manually. Items added to this list can either be module names or full paths to module files.&#x20;

### Variables

The variables list allows you to define zero or more variables to load in the PowerShell runspaces for the environment. This list can consist of variable names from the [variable configuration](../platform/variables.md).&#x20;

You can also use wild cards (`*`) to bring in multiple variables that match a pattern.

## Using Environments

Environments can be used across the platform.&#x20;

### APIs

To select the environment to use, modify the `settings.ps1` file and include the `-ApiEnvironment` parameter of `Set-PSUSetting`. It needs to be the name of the environment.&#x20;

### Automation

Each script, job and schedule can use an environment. You can define environments for scripts by modifying the `scripts.ps1` and setting the `-Environment` parameter of `New-PSUScript`. To set the environment of a schedule, set the `-Environment` parameter of `New-PSUSchedule` in `schedules.ps1`. When invoking a script, you can also choose an environment to use.&#x20;

### Dashboards

To use a particular environment for a dashboard, set the `-Environment` parameter of `New-PSUDashboard` in `dashboards.ps1`.

### Security

By default, authentication and authorization happen within the `Universal.Server.exe` process. To run these out of process, you can select an environment by setting the `-SecurityEnvironment` parameter of `Set-PSUSetting` in `settings.ps1`.&#x20;

## Integrated Environment

{% hint style="info" %}
The integrated environment does not support running as alternate credentials.&#x20;
{% endhint %}

The integrated environment uses the PowerShell Universal server process directly rather than starting external PowerShell processes to service requests.&#x20;

The integrated environment is easier to configure and use than having multiple disparate environments. You will also see a performance improvement because there is no need to serialize and communicate via interprocess communication.&#x20;

The downside is that you cannot elevate to alternate credentials or use alternate PowerShell versions. You will be using the current version of the PowerShell Universal server's PowerShell SDK.&#x20;

### Configuring

The integrated environment is always available and you do not need to configured it directly. If you do want to import modules or set up persistent runspaces, you can set settings for the integrated environment in `environments.ps1`.&#x20;

{% code title=".universal\environments.ps1" %}
```powershell
New-PSUEnvironment -Name 'Integrated' -Path 'none' -Modules @('ActiveDirectory')
```
{% endcode %}

### APIs

To set the integrated environment, you can use the `Set-PSUSetting` in `settings.ps1`.&#x20;

{% code title=".universal\settings.ps1" %}
```powershell
Set-PSUSetting -ApiEnvironment 'Integrated'
```
{% endcode %}

### Automation

You can assign the integrated environment to scripts and schedules. You can also set the integrated environment as the default environment for the platform.&#x20;

```powershell
Set-PSetting -DefaultEnvironment 'Integrated'
```

You can also choose the integrated environment from the run dialog.&#x20;

![](<../.gitbook/assets/image (224).png>)

### Dashboards

You can run dashboards in the integrated environment. Select the integrated environment from the environment drop down.&#x20;

![](<../.gitbook/assets/image (225).png>)

## API

* [New-PSUEnvironment](../cmdlets/New-PSUEnvironment.txt)
* [Get-PSUEnvironment](../cmdlets/Get-PSUEnvironment.txt)
* [Remove-PSUEnvironment](../cmdlets/Remove-PSUEnvironment.txt)
