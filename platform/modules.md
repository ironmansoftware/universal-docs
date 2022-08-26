---
description: Module management for PowerShell Universal.
---

# Modules

The Modules page provides information about the modules installed in the system.&#x20;

## Viewing Modules

You can view and search the modules accessible by PowerShell Universal by visiting the Platform \ Modules page. Searching provides a wildcard result of the modules found in each of the environments defined within PowerShell Universal.&#x20;

![](<../.gitbook/assets/image (310) (1) (1).png>)

## Install Modules from the Gallery

Modules can be installed from the PowerShell Gallery. To search for a module, you can change the drop down next to the search box from Local to PowerShell Gallery. Searches conducted will run against the Gallery rather than locally.&#x20;

Once a module is found, you'll be able to click the Install button to save it locally. Modules installed in this method will be installed into the Repository directory under Modules.&#x20;

## Package Sources

PowerShell Universal integrates with the `PackageManagement` module and will automatically pick up on registered package sources. For example, you can register a package source with the command below.&#x20;

```powershell
Register-PackageSource -Name MyNuGet -Location https://www.nuget.org/api/v2 -ProviderName NuGet
```

Once the source has been registered, it will be shown within the drop down on the modules page.&#x20;

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## Creating Modules&#x20;

You can also create modules directly in PowerShell Universal. These modules will be created in the Repository directory under Modules.&#x20;

These modules will be available in all environments.

To create a new module navigate to Platform \ Modules and click Create New Module. Define the module name and version.&#x20;

![](<../.gitbook/assets/image (396).png>)

Once created, the module will be listed under Universal Modules with the option to edit properties and content as well as delete the module.&#x20;

![](<../.gitbook/assets/image (364).png>)

When editing the module, it will open a code editor where you can define functions, variables and aliases to export.&#x20;

![](<../.gitbook/assets/image (393).png>)

## Module Information

This section includes information about certain modules and their use within PowerShell Universal.

### ActiveDirectory

The `ActiveDirectory` module supports native PowerShell 7 support when using the 1.0.1.0 version. When using the 1.0.0.0 version, the Windows Compatibility layer is used when running the commands in PowerShell 7 and the Integrated environment. This can cause problems within PowerShell Universal. Our guidance for this module is as follows.&#x20;

#### Windows Server 2019 and above

Update the `ActiveDirectory` module to version 1.0.1.0 which has PowerShell Core support

#### Windows Server 2016 and below

Choose from 1 of 2 available workarounds:

* Include the `-SkipEditionCheck` parameter with **Import-Module** when importing the ActiveDirectory module
* Use the Windows PowerShell 5.1 environment instead of Integrated/PowerShell Core

#### Further Reading

[https://devblogs.microsoft.com/powershell/increased-windows-modules-coverage-with-powershell-core-6-1/](https://devblogs.microsoft.com/powershell/increased-windows-modules-coverage-with-powershell-core-6-1/)

