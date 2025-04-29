---
description: Module management for PowerShell Universal.
---

# Modules

The Modules page provides information about the modules installed in the system.

## Viewing Modules

You can view and search the modules accessible by PowerShell Universal by visiting the Platform \ Modules page. Searching provides a wildcard result of the modules found in each of the environments defined within PowerShell Universal.

![](<../.gitbook/assets/image (265).png>)

## Install Modules from the Gallery

Modules can be installed from the PowerShell Gallery. To search for a module, you can change the drop down next to the search box from Local to PowerShell Gallery. Searches conducted will run against the Gallery rather than locally.

Once a module is found, you'll be able to click the Install button to save it locally. Modules installed in this method will be installed into the Repository directory under Modules.

## Package Sources

PowerShell Universal integrates with the `PackageManagement v3` module and will automatically pick up on registered package sources. For example, you can register a package source with the command below.

```powershell
Register-PSResourceRepository -Name MyNuGet -Uri https://www.nuget.org/api/v2
```

Once the source has been registered, it will be shown within the drop down on the modules page.

<figure><img src="../.gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>

## Creating Modules

You can also create modules directly in PowerShell Universal. These modules will be created in the Repository directory under Modules.

These modules will be available in all environments.

To create a new module navigate to Platform \ Modules and click Create New Module. Define the module name and version.

![](<../.gitbook/assets/image (319).png>)

Once created, the module will be listed under Universal Modules with the option to edit properties and content as well as delete the module.

![](<../.gitbook/assets/image (54).png>)

When editing the module, it will open a code editor where you can define functions, variables and aliases to export.

![](<../.gitbook/assets/image (455).png>)

## Modules with Universal Resources

{% hint style="info" %}
An example module can be [found here](https://github.com/ironmansoftware/universal-modules).
{% endhint %}

### Install

Modules can contain PowerShell Universal resources such as scripts, APIs and apps. Adding these modules to your environment will automatically add these resources to your PowerShell Universal instance. These resources will be read-only within the environment. To remove them, you will have to remove the module.

Within the Admin Console, click Platform \ Modules and then select PowerShell Universal Modules.

<figure><img src="../.gitbook/assets/image (110).png" alt=""><figcaption><p>PowerShell Universal Modules</p></figcaption></figure>

Click the download button on the left size of the module to install it. Once installed, read-only resources will be added to your environment.

<figure><img src="../.gitbook/assets/image (456).png" alt=""><figcaption><p>Windows System Information App</p></figcaption></figure>

You can also save modules directly to the PowerShell Universal repository folder.

```powershell
Save-Module Universal.Apps.WindowsSystemInformation -Path $Env:ProgramData\UniversalAutomation\Repository\Modules
```

### Create

Below is an example of the layout of a Universal module. If the module contains the `.universal` folder, resources will be loaded from it automatically.

```
.universal 
    scripts.ps1
PSUModule.psd1
PSUModule.psm1
```

Resources cannot use paths and must use the module and command name to associate resources with their respective scripts.

For example, the above `scripts.ps1` file would have to be written such as this.

```powershell
New-PSUScript -Module 'PSUModule' -Command 'Start-MyScript'
```

Within `PSUModule.psm1`, you would need to define the `Start-MyScript` function. This is the function that will be called when running the script.

```powershell
function Start-MyScript {

}
```

### Publish

When creating modules that extend PowerShell Universal, you can include the `PowerShellUniversal` tag in your module manifest for them to be listed within the [PowerShell Universal Modules page](https://ironmansoftware.com/powershell-universal/modules) and within the PSU admin console.

[Publish modules to the PowerShell Gallery](https://jeffbrown.tech/how-to-publish-your-first-powershell-gallery-package/) in order to share them with others.

## Manually Install Modules

PowerShell Universal will add the repository's `Modules` directory to the `$ENV:PSModulePath` for all environments. Adding modules to this directory will ensure the module is available to any PowerShell process running with PowerShell Universal.

## Module Information

This section includes information about certain modules and their use within PowerShell Universal.

### ActiveDirectory

The `ActiveDirectory` module supports native PowerShell 7 support when using the 1.0.1.0 version. When using the 1.0.0.0 version, the Windows Compatibility layer is used when running the commands in PowerShell 7 and the Integrated environment. This can cause problems within PowerShell Universal. Our guidance for this module is as follows.

#### Windows Server 2019 and above

Update the `ActiveDirectory` module to version 1.0.1.0 which has PowerShell Core support

#### Windows Server 2016 and below

Choose from 1 of 2 available workarounds:

* Include the `-SkipEditionCheck` parameter with **Import-Module** when importing the ActiveDirectory module
* Use the Windows PowerShell 5.1 environment instead of Integrated/PowerShell Core

#### Further Reading

{% embed url="https://devblogs.microsoft.com/powershell/increased-windows-modules-coverage-with-powershell-core-6-1/" %}

### Exchange

On-premises Microsoft Exchange can be managed using remote sessions in PowerShell. If you are using sessions in apps, you will want to consider managing the session in a way to prevent having to open a new session for every request. This greatly improves performance. The below example uses the `$Cache:` scope to persist the session across requests.&#x20;

While this example uses PSSessions and Exchange, you could use the same pattern for other types of persistent connections.&#x20;

```powershell
$Cache:ExchangeServer = ''
$Cache:ExchangeCredential = ''
$Cache:ExchangeSessionInfo = @{

    Authentication    = 'Kerberos'
    ConfigurationName = 'Microsoft.Exchange'
    ConnectionUri     = 'https://{0}/PowerShell/' -f $Cache:ExchangeServer
    Credential        = $Cache:ExchangeCredential
    WarningAction     = 'SilentlyContinue'
}

#region PRIVATE FUNCTIONS

Function Script:Connect-ExchServer {
    $exchSession = New-PSSession @Cache:ExchangeSessionInfo
    Import-PSSession $exchSession -WarningAction 'SilentlyContinue'
}


Function Script:Test-ExchConnected {
    $Current = Get-PSSession | Where-Object { $_.ConfigurationName -eq 'Microsoft.Exchange' }
    if ($Current.State -eq 'Opened' -and $Current.Availability -eq 'Available') {
        $true
    }
    else {
        $false
    }
}

#endregion

#region PUBLIC FUNCTIONS 

Function Clear-ExchConnection {
    # called publicly in "End{}" blocks.
    Get-PSSession | Where-Object { $_.ConfigurationName -eq 'Microsoft.Exchange' } | Remove-PSSession -ErrorAction $Cache:ErrorAction
    Get-Module | Where-Object { $_.Description -match $Cache:ExchangeServer } | Remove-Module -Force -ErrorAction $Cache:ErrorAction
}


Function Confirm-ExchConnected {
     # called publicly in "Begin{}" blocks, or just before Exhange actions in functions or scripts.
    if (!( Test-ExchConnected )) {
        Clear-ExchConnection
        Connect-ExchServer
    }
}

#endregion

function Invoke-ExampleExchFunction {
    Param (
        $something
    )

    Begin {
        $null = Confirm-ExchConnected
    }
    
    Process {
        return $something
    }
    
    End {
        Clear-ExchConnection
    }
}
```

## Validated Module Versions

The below module versions have been validated against PowerShell Universal. Module validation ensures that these modules load and interact with their respective services.&#x20;

| Module                         | Module Version | PSU Version | PSU Environments         |
| ------------------------------ | -------------- | ----------- | ------------------------ |
| Microsoft.Graph.Authentication | 2.26.1         | 5.5.2       | PowerShell 7             |
| ExchangeOnlineManagement       | 3.7.2          | 5.5.2       | PowerShell 7             |
| MicrosoftTeams                 | 6.9.0          | 5.5.2       | PowerShell 7             |
| Az.Accounts                    | 4.1.0          | 5.5.2       | PowerShell 7, Integrated |

