---
description: Information about execution environments.
---

# Environments

Environments allow you to define an executable, arguments, modules and variables to use when running scripts, hosting APIs and dashboards. 

Environments are stored within the `environments.ps1` file. 

## Configuring Environments

To configure environments, you can use the Settings \ Environments page. 

![](../.gitbook/assets/image%20%28136%29.png)

Environments support setting the name, path, arguments, modules and variables.

![](../.gitbook/assets/image%20%28135%29.png)

### Name 

The name of the environment. This name will be shown through out the rest of the platform when running scripts, configuring the API host environment and hosting dashboards. 

### Path and Arguments

Environments support defining a path to an executable and arguments for that executable. These should be either PowerShell.exe or Pwsh.exe. 

You can also define modules and variables. 

### Modules

The modules list allows you to define zero or more modules to load in the PowerShell runspaces for the environment. These modules will be part of the initial session state so they will not need to be loaded manually. Items added to this list can either be module names or full paths to module files. 

### Variables

The variables list allows you to define zero or more variables to load in the PowerShell runspaces for the environment. This list can consist of variable names from the [variable configuration](../platform/variables.md). 

You can also use wild cards \(`*`\) to bring in multiple variables that match a pattern.

## Using Environments

Environments can be used across the platform. 

### APIs

To select the environment to use, modify the `settings.ps1` file and include the `-ApiEnvironment` parameter of `Set-PSUSetting`. It needs to be the name of the environment. 

### Automation

Each script, job and schedule can use an environment. You can define environments for scripts by modifying the `scripts.ps1` and setting the `-Environment` parameter of `New-PSUScript`. To set the environment of a schedule, set the `-Environment` parameter of `New-PSUSchedule` in `schedules.ps1`. When invoking a script, you can also choose an environment to use. 

### Dashboards

To use a particular environment for a dashboard, set the `-Environment` parameter of `New-PSUDashboard` in `dashboards.ps1`.

### Security

By default, authentication and authorization happen within the `Universal.Server.exe` process. To run these out of process, you can select an environment by setting the `-SecurityEnvironment` parameter of `Set-PSUSetting` in `settings.ps1`. 

## Integrated Environment

The integrated environment uses the PowerShell Universal server process directly rather than starting external PowerShell processes to service requests. 

The integrated environment is easier to configure and use than having multiple disparate environments. You will also see a performance improvement because there is no need to serialize and communicate via interprocess communication. 

The downside is that you cannot elevate to alternate credentials or use alternate PowerShell versions. You will be using the current version of the PowerShell Universal server's PowerShell SDK. 

### Configuring

The integrated environment is always available and you do not need to configured it directly. If you do want to import modules or set up persistent runspaces, you can set settings for the integrated environment in `environments.ps1`. 

```text
New-PSUEnvironment -Name 'Integrated' -Path 'none' -Modules @('ActiveDirectory')
```

### APIs

To set the integrated environment, you can use the `Set-PSUSetting` in `settings.ps1`. 

```text
Set-PSUSetting -ApiEnvironment 'Integrated'
```

### Automation

You can assign the integrated environment to scripts and schedules. You can also set the integrated environment as the default environment for the platform. 

```text
Set-PSUSetting -DefaultEnvironment 'Integrated'
```

You can also choose the integrated environment from the run dialog. 

![](../.gitbook/assets/image%20%28224%29.png)

### Dashboards

You can run dashboards in the integrated environment. Select the integrated environment from the environment drop down. 

![](../.gitbook/assets/image%20%28225%29.png)

