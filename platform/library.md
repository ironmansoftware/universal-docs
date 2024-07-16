---
description: The Universal Library of scripts, widgets, triggers and more.
---

# Library

The Universal Library is a collection of pre-built solutions for PowerShell Universal. It includes resources such as scripts, triggers, apps, and widgets. The library is installed with PowerShell Universal.&#x20;

The [library ](https://github.com/ironmansoftware/scripts/issues)is open-source, and each release of PowerShell Universal includes a copy that is downloaded during the build process. The library is registered as a PowerShell Module Repository in PowerShell Universal. It consists of a folder of `.nupkg` files for each module.&#x20;

## Installing Resources from the Library

To install resources from the library, click Platform \ Library in the Universal Admin Console. Click the Install icon to save the resource into your environment. Each solution is a PowerShell module that will be included in your Repository's module directory.&#x20;

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Universal Library Catalog</p></figcaption></figure>

Resources installed from modules, like from the Library, are marked as read-only in the Admin Console.&#x20;

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Read-Only Resource in the Admin Console</p></figcaption></figure>

## Uninstalling Resources

Once a resource is installed, you cannot remove it unless you remove the module itself. You can navigate to the Platform \ Modules page and click the Repository Modules tab to view modules installed from the library.&#x20;

Clicking the Delete icon will remove the module and any resources associated with it.&#x20;

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Repository Modules</p></figcaption></figure>

## Contributing to the Library

You can contribute your own scripts to the Universal Library. We accept pull requests on the[ Library GitHub repository](https://github.com/ironmansoftware/scripts). When a new version of PowerShell Universal is released, we update the library files and distribute them alongside the install media.&#x20;
