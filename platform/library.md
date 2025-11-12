---
description: The PowerShell Universal Gallery of scripts, widgets, triggers and more.
---

# Gallery

The Gallery is a collection of pre-built solutions for PowerShell Universal. It includes resources such as scripts, triggers, apps, and widgets. It is open-source, and the modules are published to the PowerShell Gallery. The [PowerShell Universal Gallery](https://powershelluniversal.com/gallery) provides a filtered list of resources specific to the platform.

## Installing Resources from the Gallery

### Gallery Page

The Gallery page discovers PowerShell Universal modules in the PowerShell Gallery. It will cache the results for 5 minutes to improve performance.

To install resources from the library, click Platform \ Gallery in the Universal Admin Console. Click the Install icon to save the resource into your environment. Each solution is a PowerShell module that will be included in your Repository's module directory.

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption><p>Modules in the Gallery</p></figcaption></figure>

Resources installed from modules, like from the Gallery, are marked as read-only in the Admin Console.

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Read-Only Resource in the Admin Console</p></figcaption></figure>

### Module Page

On the module page, click Galleries, and then select the PSGallery to search and download resources directly from the PowerShell Gallery feed. You will need to filter by the `PowerShellUniversal`tag to find modules specific to the platform.

## Uninstalling Resources

Once a resource is installed, you cannot remove it unless you remove the module itself. You can navigate to the Platform \ Modules page and click the Repository Modules tab to view modules installed from the library.

Clicking the Delete icon will remove the module and any resources associated with it.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Repository Modules</p></figcaption></figure>

## Contributing to the Gallery

You can contribute your own scripts to the PowerShell Universal Gallery. The PowerShell Universal Gallery automatically located modules within the PowerShell Gallery tagged with `PowerShellUniversal`. If you'd like your module to show up within the PowerShell Universal Gallery and PowerShell Universal, include this tag.

Below is an example of a manifest from the PowerShell Universal Gallery repository. You can include a GitHub repository path as the `ProjectUri` in the manifest. If you do so, the contents of the README.md file will be rendered on PowerShellUniversal.com.

```powershell
@{
    ModuleVersion = '1.0.0'
    GUID          = '59f32838-32bb-46e3-b29d-eb360292a8c9'
    Author        = 'Ironman Software'
    CompanyName   = 'Ironman Software'
    Copyright     = '(c) Ironman Software. All rights reserved.'
    Description   = 'Provides API endpoints from querying, creating, deleting and updating CIM instances.'
    PrivateData   = @{
        PSData = @{
            Tags       = @('CIM', "PowerShellUniversal", "api")
            LicenseUri = 'https://github.com/ironmansoftware/scripts/tree/main/LICENSE'
            ProjectUri = 'https://github.com/ironmansoftware/scripts/tree/main/APIs/PowerShellUniversal.API.CIM'
            IconUri    = 'https://raw.githubusercontent.com/ironmansoftware/scripts/main/images/script.png'
        }
    }
}
```

### Licensed Modules

{% hint style="info" %}
Licensed modules are currently in preview.
{% endhint %}

As of PowerShell Universal 5.2, you can now include a `PSULicensed` option in the `PSData` section of your module manifest. If the module is licensed, it will not load it without a license file specific to the module being loaded. License files are currently generated manually by Ironman Software for module authors. Please contact Ironman Software support for more information.

```powershell
@{
    ModuleVersion = '1.0.0'
    GUID          = '59f32838-32bb-46e3-b29d-eb360292a8c9'
    Author        = 'Ironman Software'
    CompanyName   = 'Ironman Software'
    Copyright     = '(c) Ironman Software. All rights reserved.'
    Description   = 'Provides API endpoints from querying, creating, deleting and updating CIM instances.'
    PrivateData   = @{
        PSData = @{
            Tags       = @('CIM', "PowerShellUniversal", "api")
            LicenseUri = 'https://github.com/ironmansoftware/scripts/tree/main/LICENSE'
            ProjectUri = 'https://github.com/ironmansoftware/scripts/tree/main/APIs/PowerShellUniversal.API.CIM'
            IconUri    = 'https://raw.githubusercontent.com/ironmansoftware/scripts/main/images/script.png'
            PSULicensed = $true
        }
    }
}
```

If a licensed module is installed but no license is provided, PowerShell Universal will not load resources from the module. Do note that any generic PowerShell functions, aliases and variables exposed by the module will be available. Apps, scripts, APIs or other PowerShell Universal features will not be loaded.

Licensed modules currently provide no mechanism to obfuscate your PowerShell scripts or restrict users from removing the licensing flag. We recommend including a standard EULA to ensure that users are legally accountable for manipulating these files to bypass the licensing.
