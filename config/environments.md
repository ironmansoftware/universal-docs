---
description: Information about execution environments.
---

# Environments

Environments allow you to define an executable, arguments, modules and variables to use when running scripts, hosting APIs and dashboards.&#x20;

Environments are stored within the `environments.ps1` file.&#x20;

## Configuring Environments

To configure environments, you can use the Settings \ Environments page.&#x20;

![Environments Page](<../.gitbook/assets/image (363).png>)

Environments support setting the name, path, arguments, modules and variables.

![](<../.gitbook/assets/image (132).png>)

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

### PSModulePath

You can use the `-PSModulePath` parameter of `New-PSUEnvironment` to configure additional PSModulePaths to include within the environment.&#x20;

### Startup Scripts

![](<../.gitbook/assets/image (1) (1) (2).png>)

Startup scripts are run once when the environment is first creates a runspace. For APIs, this happens whenever a runspace is created to service an HTTP request. This can happen for frequently if the server is busy. For dashboards, this will happen whenever a runspace is crated to service an endpoint being run while the user views a dashboard. Busy servers and dashboards with many dynamic components will do this more frequently. For jobs, this will happen once when the job is started.&#x20;

Startup scripts are relative to the Repository folder. For example, if you had a script in your repository named `startup.ps1`, you would just list the file name in the configuration. If you had a script in a directory, you would need to include that as well.&#x20;

Platform variables are not available in startup scripts.

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

The downside is that you cannot elevate to alternate credentials or use alternate PowerShell versions. You will be using the current version of the PowerShell Universal server's PowerShell SDK. Additionally, since all the PowerShell scripts are running within the service, you can affect the stability of the platform with your PowerShell scripts.&#x20;

Please read[ Best Practices ](best-practices.md#favor-non-integrated-environments)for more information.&#x20;

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

![](<../.gitbook/assets/image (226).png>)

### Dashboards

You can run dashboards in the integrated environment. Select the integrated environment from the environment drop down.&#x20;

![](<../.gitbook/assets/image (225).png>)

### Module Support

The integrated environment works by creating multiple ruspaces within the PowerShell Universal service. Some modules do not work well when run within a single process. Below is a list of modules with known issues running within the integrated environment.&#x20;

* VMware.PowerCLI
* Az

## Agent Environment

PowerShell Universal includes an agent process that can be executed outside of the PowerShell Universal service. Similar to the Integrated environment, it uses the current version of PowerShell that PowerShell Universal includes. Unlike the integrated environment, it spawns an external process and doesn't require PowerShell 7 be installed on the target machine.&#x20;

The Agent environment also supports run as credentials.&#x20;

## Windows PowerShell Compatiblity

Windows PowerShell Compatibility is a feature of PowerShell 7. When commands and modules are not available in PowerShell 7, the platform will automatically start a Windows PowerShell process in the background and perform local remoting from the PowerShell 7 process. This achieves backwards compatibility with Windows PowerShell modules.&#x20;

You may see a warning in the environments page when this feature of PowerShell is enabled due to the implications on the PowerShell Universal platform.&#x20;

### Problems with WinPS Compatiblity in PowerShell Universal&#x20;

For each runspace opened by PowerShell Universal in which Windows PowerShell Compatibility is used, a new Windows PowerShell process will be started. These processes will only stop once the runspace is recycled.&#x20;

This greatly reduces performance due to an excessive number of processes running and memory and CPU usage attributed to serialization and remote runspace management.&#x20;

The most common cause of this is using the Active Directory 1.0.0.0 module from PowerShell 7.&#x20;

### Disabling Implicit Windows PowerShell Compatibility

You can disable implicit Windows PowerShell Compatibility by modifying the `powershell.config.json` file in `$PSHome`. You can still use Windows PowerShell Compatibility but will need to import modules using `-UseWindowsPowerShell`.

```powershell
@{ DisableImplicitWinCompat = $true } | ConvertTo-Json | Out-File "$PSHome\powershell.config.json"
```

`$PSHome` differs per PowerShell host. Running the above command line will disable WinPSCompat for the PowerShell 7 environment when run within a PowerShell 7 process. To disable it for the PowerShell Universal Integrated environment, you will need to create the `powershell.config.json` file within the PSU installation folder.&#x20;

For example, `C:\Program Filxes (x86)\Universal`.

It's also possible to provide the `--SettingsFile` parameter to `pwsh.exe` in order to load a `powershell.config.json` file from another location.

### Cleanly Using Windows PowerShell Compatibility

If required, you can remove the Windows Compatibility runspace after executing a command using the feature. This will remove the Windows PowerShell process. Each time this endpoint is run, it will need to re-establish the session.

```powershell
Import-Module PSScheduledJob -UseWindowsPowerShell
Get-ScheduledJob | Out-Null
Get-PSSession -Name 'WinPSCompatSession' | Remove-PSSession
```

You can learn more about [Windows PowerShell Compatibility here](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about\_windows\_powershell\_compatibility?view=powershell-7.2).

## API

* [New-PSUEnvironment](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-PSUEnvironment.txt)
* [Get-PSUEnvironment](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Get-PSUEnvironment.txt)
* [Remove-PSUEnvironment](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/Remove-PSUEnvironment.txt)
