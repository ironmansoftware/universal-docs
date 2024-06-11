---
description: Persistence for PowerShell Universal.
---

# Persistence

PowerShell Universal stores job output and input, identities and app tokens within the database.

## SQLite

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

## LiteDB

Using LiteDB, PowerShell Universal stores all data within a single file database local to the PowerShell Universal application.

To configure the database location for LiteDB you can edit the `appsettings.json` file or set the file path during installation if using the MSI. By default, the database is stored in the ProgramData directory. Update this setting to change the database location.

```json
"ConnectionString": "filename=%ProgramData%\\UniversalAutomation\\database.db;upgrade=true",
```

LiteDB does not support multiple instances of PowerShell Universal connecting to the same database.

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

We support Microsoft SQL Server 2016 and onwards.

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

You can enable PostgreSQL will the `PostgreSQL` plugin.&#x20;

```json
 "Plugins": [
    "PostgreSQL"
  ],
  "Data": {
    "ConnectionString": "Host=PGhostname; Database=PGdatabase; User Id=PGusername; Password=PGpassword!;Port=5432",
  },
```

## Data Migration

PowerShell Universal includes a data migration tool for moving data from LiteDB to SQL. You can find `DataMigration.exe` in the installation folder.

You will need access to the LiteDB database and the SQL server in order to run the tool. You cannot have PowerShell Universal running while migrating the data.

Below is an example of how to run the data migration tool.

```
DataMigration.exe -l C:\ProgramData\UniversalAutomation\database.db -s 'Server=(localdb)\mssqllocaldb;Database=PSU;Trusted_Connection=True;'
```

By default, the migration tool will install the schema for the database. You can use the `--noschema` parameter to prevent this from happening.

### Command Line Arguments

<table><thead><tr><th>Argument</th><th width="406">Description</th><th>Required</th></tr></thead><tbody><tr><td>-l, --litedb</td><td>Path to the LiteDB database file.</td><td>yes</td></tr><tr><td>-s, --sql</td><td>Connection string for the SQL database</td><td>yes</td></tr><tr><td>-c, --clean</td><td>Drop the database before migrating</td><td>no</td></tr><tr><td>--noschema</td><td>Skip schema migrations and only transfer the data</td><td>no</td></tr><tr><td>--continueonerror</td><td>Continue migrating items even if there is an error</td><td>no</td></tr></tbody></table>
