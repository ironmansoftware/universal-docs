---
description: Persistence for PowerShell Universal.
---

# Persistence

PowerShell Universal stores job output and input, identities and app tokens within the database.

## SQLite

{% hint style="warning" %}
SQLite does not scale and is only recommended for small instances or testing. We recommend selecting MS SQL or PostgreSQL for production environments.
{% endhint %}

When using SQLite, PowerShell Universal stores all data within a single file database local to the PowerShell Universal application. We recommend SQLite over LiteDB for new installations as it is more widely used and supported.

You can configure SQLite by updating the `appsettings.json` file.

```json
 "Plugins": [
    "SQLite"
  ],
  "Data": {
    "ConnectionString": "Data Source=%ProgramData%\\UniversalAutomation\\psu.db",
  },
```

### Troubleshooting Large Database Sizes

Large SQLite databases can be the result of long job history, jobs that write excessively to pipeline output or PowerShell output streams, stale computer, process or runspace information, or large log entry tables.

As the database grows, the performance of PowerShell Universal will be affected. In order to troubleshoot what is causing this growth, use the SQLite\_Analyzer tool. You can download SQLite\_Analyzer as part of the tools ZIP on the [SQLite download page](https://www.sqlite.org/download.html).

Once downloaded, run the analyzer against your PowerShell Universal database file to get an extensive list of information about the status of your database. We recommend stopping PowerShell Universal before running the following command.

```
.\sqlite_analyzer.exe C:\ProgramData\UniversalAutomation\database.db
```

The command will include information about the size of tables and indexes within the database. This will help to pinpoint exactly where the large amount of data is being stored.

### Reducing Database Size

SQLite will retain unused space in the freelist within the database after records are updated or deleted. Databases that run many jobs or have been running for a longer duration may have a large database file with a large freelist. You can run the `sqlite_analyzer` tool to determine how much space is used by the free list.

The example database below is 23 GB in size but 99.946% of it is unused space.

```
/** Disk-Space Utilization Report For ./psu.db

Page size in bytes................................ 4096      
Pages in the whole file (measured)................ 5953770   
Pages in the whole file (calculated).............. 5953770   
Pages that store data............................. 3230         0.054% 
Pages on the freelist (per header)................ 5950539     99.946% 
Pages on the freelist (calculated)................ 5950539     99.946% 
Pages of auto-vacuum overhead..................... 0            0.0% 
Number of tables in the database.................. 66        
Number of indices................................. 48        
Number of defined indices......................... 47        
Number of implied indices......................... 1         
Size of the file in bytes......................... 24386641920
Bytes of user payload stored...................... 6611527      0.027% 
```

To reclaim this space, SQLite can use the vacuum feature to rebuild the database and reduce the size of the freelist. `auto-vacuum` is not enabled in PowerShell Universal databases. If you are experiencing issues with database size, you can run the `VACUUM;` command within the Support Tool's Database tool.

{% hint style="warning" %}
We recommend backing up your database file before performing a VACUUM. This command rebuilds the database, defragments it and removes the freelist from the file.
{% endhint %}

Click Help \ Support Tools \ Tools \ Database \ Execute. Enter the following command and execute it.

```
VACUUM;
```

## SQL

{% hint style="info" %}
SQL support requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

You can configure PowerShell Universal to store data within a Microsoft SQL Database. This allows you to scale out your database and PowerShell Universal instances. PowerShell Universal will automatically run jobs across the pool of agents. You can update the `appsettings.json` file for PowerShell Universal as follows to connect to a central SQL server.

```json
  "Plugins": [
    "SQL"
  ],
  "Data": {
    "ConnectionString": "Server=(localdb)\\mssqllocaldb;Database=PSUv3;Integrated Security=true;",
  },
```

The PowerShell Universal instances will share a single job queue and only one instance will run a job either on the schedule, as a trigger, or manually. All data about jobs will be stored in the centralized database.

### Azure SQL

We recommend using Azure Managed Identities when working with Azure SQL. An example connection string is shown below.

```
Server=tcp:psudb.database.windows.net,1433;Initial Catalog=psu;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;Authentication=Active Directory Managed Identity;
```

A walkthrough on how to use [Managed Identity for Azure SQL can be found here](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/tutorial-windows-vm-access-sql).

### Manual Schema Install\Update

In some environments, the PSU service may not have access to create schema in the database. In this scenario, you can manually install and update the schema by executing SQL files included with PowerShell Universal. Within the PowerShell Universal installation folder, you will find a `SQL` directory that includes two SQL files.

Run these files against your database prior to upgrading PowerShell Universal. You will need to stop PowerShell Universal while you are doing this. You can run them in any order. Both scripts are idempotent.

By default, PowerShell Universal will attempt to update the schema of the database. To completely disable this feature, you can set the `RunMigrations` setting to false in appsettings.json.

```json
"Data": {
   "RunMigrations": false
}
```

### Frequently Asked Questions

#### Database Account Privileges

_What is the maximum permission for a database user account needed during installs or upgrades?_

During the startup of the PowerShell Universal server, the database will be installed and upgraded, if required. If the database already exists, you will need `db_owner` in order to create and modify tables. If the database does not yet exist, you will need `dbcreator` .

_What is the maximum permission needed once the database(s) has been created for ongoing daily activities?_

PowerShell Universal performs limited database operations during daily activities. This consist of inserting, updating, deleting and viewing data in the tables created. You will only need the following roles: `db_datawriter`, `db_datareader`

#### Database & Operating System Install & Support

_Which versions of SQL Server are supported? Is there a minimum version required?_

PowerShell Universal supports Microsoft SQL Server 2016 and onwards.

_Which database compatibility versions do you support?_

PowerShell Universal supports require [database compatbility version 130 ](https://learn.microsoft.com/en-us/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database?view=sql-server-ver16)of later.

_Do any other SQL Server components need to be installed beside the Database Engine?_

None

_Which versions of Windows Server are supported?_

Currently Supported versions by Microsoft - Windows Server 2016 and onwards. Currently, the extended end date for support for 2012 R2 from Microsoft is October 10, 2023, at which time we will drop support for the operating system.

#### Database Maintenance & Backup

_How quickly does the data need to be recovered?_

Data is primarily for reporting, aside from app tokens, so data doesn't need to be immediately recovered. Depending on the use of the app tokens, some systems may lose access to the server when the database is being recovered.

#### Database Design

_How large will the database(s) be for the initial load?_

The initial database does not include a large set of initial data and primarily will only take the space of the schema.

_What is the estimated growth per month/year of each database?_

The estimated growth depends on many factors that include the number of jobs run per month, amount of job log and pipeline output stored, and how aggressive data is groomed.

Database size rarely grows over 2 GB in size with the default settings. Extending groom settings to contain a longer history of jobs, running jobs more frequently and storing data like terminal history can increase the database size.

_Does your application support use of SQL Server compression (Row or Page level)?_

Yes. We use a standard database client and has no limitation on row and page level compression.

#### Database Usage

_Is this a transactional (OLTP) or reporting (OLAP) database?_

This is primarily a reporting database that includes information like job history, job output and app tokens.

_What is the total number of user/device connections?_

One connection pool per PSU server. 1024 connections maximum per server.

_What is the maximum number of concurrent user/device connections?_

One connection pool per PSU server. 1024 connections maximum per server.

## PostgreSQL

You can enable PostgreSQL will the `PostgreSQL` plugin.

```json
 "Plugins": [
    "PostgreSQL"
  ],
  "Data": {
    "ConnectionString": "Host=PGhostname; Database=PGdatabase; User Id=PGusername; Password=PGpassword!;Port=5432",
  },
```
