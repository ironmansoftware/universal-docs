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

### Frequently Asked Questions

#### Database Account Privileges&#x20;

_What is the maximum permission for a database user account needed during installs or upgrades?_

During the startup of the PowerShell Universal server, the database will be installed and upgraded, if required. If the database already exists, you will need `db_owner` in order to create and modify tables. If the database does not yet exist, you will need `dbcreator` .&#x20;

_What is the maximum permission needed once the database(s) has been created for ongoing daily activities?_

PowerShell Universal performs limited database operations during daily activities. This consist of inserting, updating, deleting and viewing data in the tables created. You will only need the following roles: `db_datawriter`, `db_datareader`

#### Database & Operating System Install & Support&#x20;

_Which versions of SQL Server are supported? Is there a minimum version required?_

We support Microsoft SQL Server 2016 and onwards.&#x20;

_Do any other SQL Server components need to be installed beside the Database Engine?_

None

_Which versions of Windows Server are supported?_

Currently Supported versions by Microsoft - Windows Server 2012 R2 and onwards. Currently, the extended end date for support for 2012 R2 from Microsoft is October 10, 2023, at which time we will drop support for the operating system.

#### Database Maintenance & Backup

_How quickly does the data need to be recovered?_

Data is primarily for reporting, aside from app tokens, so data doesn't need to be immediately recovered. Depending on the use of the app tokens, some systems may lose access to the server when the database is being recovered.

#### Database Design

_How large will the database(s) be for the initial load?_

The initial database does not include a large set of initial data and primarily will only take the space of the schema.&#x20;

_What is the estimated growth per month/year of each database?_

The estimated growth depends on many factors that include the number of jobs run per month, amount of job log and pipeline output stored, and how aggressive data is groomed.

Database size rarely grows over 2 GB in size with the default settings. Extending groom settings to contain a longer history of jobs, running jobs more frequently and storing data like terminal history can increase the database size.&#x20;

_Does your application support use of SQL Server compression (Row or Page level)?_

Yes. We use a standard database client and has no limitation on row and page level compression.

#### Database Usage

_Is this a transactional (OLTP) or reporting (OLAP) database?_

This is primarily a reporting database that includes information like job history, job output and app tokens.&#x20;

_What is the total number of user/device connections?_

One connection pool per PSU server. 1024 connections maximum per server.

_What is the maximum number of concurrent user/device connections?_

One connection pool per PSU server. 1024 connections maximum per server.
