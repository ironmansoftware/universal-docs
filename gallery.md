---
description: Information about the PowerShell Universal Gallery.
---

# Gallery

Similar to the PowerShell Gallery, the PowerShell Universal Gallery provides a way to share modules built for PowerShell Universal with the community. It is managed via a GitHub repository and published as a NuGet feed for consumption by PSResourceGet.&#x20;

## GitHub&#x20;

You can view all the source code for modules in the Gallery on [GitHub](https://github.com/ironmansoftware/scripts). Feel free to open issues and submit pull requests.

## NuGet Feed

The PowerShell Universal Gallery is published as a NuGet feed at [https://gallery.powershelluniversal.com/feed/index.json](https://gallery.powershelluniversal.com/feed/index.json).&#x20;

You will need the `Microsoft.PowerShell.PSResourceGet` module in order to register it as a provider as the feed is NuGet v3.&#x20;

```powershell
Install-Module 
Register-PSResourceRepository -Name 'PSUGallery' -Uri 'https://gallery.powershelluniversal.com/feed/index.json' -Trusted
```

## Module Catalog

The Gallery is also published as a module catalog on [PowerShellUniversal.com](https://powershelluniversal.com/modules).
