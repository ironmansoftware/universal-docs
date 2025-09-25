---
description: >-
  Computers are PowerShell Universal instances connected to the same database
  and git repository.
---

# Computers

{% hint style="info" %}
This feature requires a license. Each computer requires a license.
{% endhint %}

PowerShell Universal can connect multiple instances of the application to the same SQL database and git repository. Configuration files will be synchronized across the nodes via the remote repository. Jobs, computer groups, identities and app tokens will all be stored within the database and are visible on any accessible nodes.

## Connecting New Computers

Once a single node has been setup with a [SQL database](../config/persistence.md) and git repository, additional computer can be connected by specifying the SQL connection string in `appsettings.json`. See [App Settings](../config/settings.md) for information about settings. Configuration files will automatically be pull from the git remote on server startup and will setup the node with the same options as the other servers within the farm.

## Docker

Note that Docker containers will have a unique computer name on startup. It's recommended to set the `NodeName` setting in App Settings to set a static node name to avoid have many randomly generated computer names added to the database.

## Tags

Computers will receive tags based on the several aspects of the service. These include:

* Domain
* User Name
* Operating System

Computer tags are used to assign computers to certain computer groups. You can use built in tags or define custom tags to group similar computers together.&#x20;

## Computer Groups

Computer groups are a collection of computers that share similar features. Each group accepts a set of tags that are required for the computers in the group. This will ensure that only certain scripts, APIs or apps run on particular groups.

Computer groups can be defined in the Admin console under Platform \ Computers in the Groups tab or with the `New-PSUComputerGroup` cmdlet. The below example creates a computer group of all the Windows computers in your environment. You could do something similar for Linux.

```powershell
New-PSUComputerGroup -Name Windows -Tags @("windows")
```

If you have a custom tag, for example a network name like ironman.eu.local, you could assign those tags to certain computers. To group them together, create a computer group using that tag.

<figure><img src="../.gitbook/assets/image (321).png" alt=""><figcaption></figcaption></figure>

```powershell
New-PSUComputerGroup -Name Windows -Tags @("ironman.eu.local")
```

<figure><img src="../.gitbook/assets/image (324).png" alt=""><figcaption></figcaption></figure>

Once a computer group is defined, APIs, scripts, schedules, jobs and apps can be restricted to certain nodes. The following app only runs on Windows nodes.

```powershell
New-PSUApp -Name 'Windows' -FilePath 'app.ps1' -BaseUrl '/app' -ComputerGroup Windows
```

## Maintenance Mode

Computers can be set in maintenance mode. When a computer is in maintenance mode, it will not run scheduled jobs.
