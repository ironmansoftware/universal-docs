---
description: Persistence for PowerShell Universal.
---

# Persistence

PowerShell Universal stores job output and input, identities and app tokens within the database.&#x20;

## LiteDB

By default, PowerShell Universal stores all data within a single file database local to the PowerShell Universal application.&#x20;

### Configuring LiteDB

To configure the database location for LiteDB you can edit the `appsettings.json` file or set the file path during installation if using the MSI. By default, the database is stored in the ProgramData directory. Update this setting to change the database location.&#x20;

```json
"ConnectionString": "filename=%ProgramData%\\UniversalAutomation\\database.db;upgrade=true",
```

LiteDB does not support multiple instances of PowerShell Universal connecting to the same database.&#x20;

## SQL&#x20;

{% hint style="info" %}
This feature requires a [license](../licensing.md).
{% endhint %}

You can configure PowerShell Universal to store data within a Microsoft SQL Database. This allows you to scale out your database and PowerShell Universal instances. PowerShell Universal will automatically run jobs across the pool of agents. You can update the `appsettings.json` file for PowerShell Universal as follows to connect to a central SQL server.&#x20;

```json
  "Plugins": [
    "SQL"
  ],
  "Data": {
    "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
    "ConnectionString": "Server=(localdb)\\mssqllocaldb;Database=PSUv3;Integrated Security=true;",
    "GitRemote": "",
    "GitUserName": "",
    "GitPassword": "",
    "GitBranch": "",
    "GitSyncBehavior": "TwoWay",
    "GitInitializeBehavior": "",
    "ConfigurationScript": ""
  },
```

The PowerShell Universal instances will share a single job queue and only one instance will run a job either on the schedule, as a trigger, or manually. All data about jobs will be stored in the centralized database.&#x20;
