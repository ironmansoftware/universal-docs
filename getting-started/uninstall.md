---
description: Uninstall PowerShell Universal
---

# Uninstall

## Application Files

Depending on how you installed PowerShell Universal, you will need to uninstall the application files.&#x20;

### ZIP Installation

If you installed using a provided ZIP file, you can simply stop the PowerShell Universal process or service and delete the folder you extracted to.&#x20;

### MSI Installation

If you installed with the Windows MSI, uninstall the application from Add\Remove Programs.&#x20;

### Module Installation&#x20;

The Universal module installs the application files to the following locations by default.&#x20;

#### Windows&#x20;

* `%ProgramData%\PowerShellUniversal`

#### Linux and Mac OS

* `%HOME%/.PowerShellUniversal`

## Configuration Files

Configuration files are stored in the repository folder. Once you have removed the application files, you can delete the configuration files. They are stored in the following locations by default:&#x20;

### Windows&#x20;

* `%ProgramData%\PowerShellUniversal`
* `%ProgramData%\UniversalAutomation`

### Linux

* `%HOME%/.PowerShellUniversal/`

### Mac OS&#x20;

* `%HOME%/.PowerShellUniversal/`

### Desktop

* `%AppData%\PowerShellUniversal`

## Database

Removing the database depends on the database type used.&#x20;

### LiteDB

LiteDB databases are stored in a single file on the file system.

#### Windows&#x20;

* `%ProgramData%\PowerShellUniversal\database.db`

#### Linux and Mac OS

* `%HOME%/.PowerShellUniversal/database.db`

### SQL

SQL databases are stored on your SQL server and will require you to manually remove the database.&#x20;

## IIS&#x20;

You may need to uninstall the IIS App Pool and Website when removing PowerShell Universal. &#x20;
