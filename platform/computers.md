---
description: >-
  Computers are PowerShell Universal instances connected to the same database
  and git repository.
---

# Computers

{% hint style="info" %}
This feature requires a license. Each computer requires a license.&#x20;
{% endhint %}

PowerShell Universal can connect multiple instances of the application to the same SQL database and git repository. Configuration files will be synchronized across the nodes via the remote repository. Jobs, computer groups, identities and app tokens will all be stored within the database and are visible on any accessible nodes.&#x20;

## Connecting New Computers

Once a single node has been setup with a [SQL database](../config/persistence.md) and git repository, additional computer can be connected by specifying the SQL connection string in `appsettings.json`. See [App Settings](../config/settings.md) for information about settings. Configuration files will automatically be pull from the git remote on server startup and will setup the node with the same options as the other servers within the farm.&#x20;

## Docker&#x20;

Note that Docker containers will have a unique computer name on startup. It's recommended to set the `NodeName` setting in App Settings to set a static node name to avoid have many randomly generated computer names added to the database.&#x20;

## Tags&#x20;

Computers will receive tags based on the several aspects of the service. These include:&#x20;

* Domain
* User Name
* Operating System&#x20;

## Computer Groups

Computer groups are a collection of computers that share similar features. Each group accepts a set of tags that are required for the computers in the group. This will ensure that only certain scripts, APIs or apps run on particular groups.&#x20;

Computer groups can be defined in the Admin console under Platform \ Computers in the Groups tab or with the `New-PSUComputerGroup` cmdlet.&#x20;

```powershell
New-PSUComputerGroup -Name Windows -Tags @("windows")
```

Once a computer group is defined, APIs, scripts, schedules, jobs and apps can be restricted to certain nodes. The following app only runs on Windows nodes.&#x20;

```powershell
New-PSUApp -Name 'Windows' -FilePath 'app.ps1' -BaseUrl '/app' -ComputerGroup Windows
```

## Maintenance Mode

Computers can be set in maintenance mode. When a computer is in maintenance mode, it will not run scheduled jobs.&#x20;
