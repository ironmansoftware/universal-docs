---
description: Module management for PowerShell Universal.
---

# Modules

The Modules page provides information about the modules installed in the system.&#x20;

## Viewing Modules

You can view and search the modules accessible by PowerShell Universal by visiting the Platform \ Modules page. Searching provides a wildcard result of the modules found in each of the environments defined within PowerShell Universal.&#x20;

![](<../.gitbook/assets/image (297) (1) (1).png>)

## Install Modules from the Gallery

{% hint style="info" %}
Available in PowerShell Universal 2.5 or later.
{% endhint %}

Modules can be installed from the PowerShell Gallery. To search for a module, you can change the drop down next to the search box from Local to PowerShell Gallery. Searches conducted will run against the Gallery rather than locally.&#x20;

Once a module is found, you'll be able to click the Install button to save it locally. Modules installed in this method will be installed into the Repository directory under Modules.&#x20;

## Creating Modules&#x20;

{% hint style="info" %}
Available in PowerShell Universal 2.5 or later.
{% endhint %}

You can also create modules directly in PowerShell Universal. These modules will be created in the Repository directory under Modules.&#x20;

These modules will be available in all environments.

To create a new module navigate to Platform \ Modules and click Create New Module. Define the module name and version.&#x20;

![](<../.gitbook/assets/image (303) (1) (1) (1) (1).png>)

Once created, the module will be listed under Universal Modules with the option to edit properties and content as well as delete the module.&#x20;

![](<../.gitbook/assets/image (301) (1) (1).png>)

When editing the module, it will open a code editor where you can define functions, variables and aliases to export.&#x20;

![](<../.gitbook/assets/image (302) (1) (1) (1) (1) (1).png>)

