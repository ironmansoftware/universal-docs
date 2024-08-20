---
description: Uninstall PowerShell Universal
---

# Uninstall

## Application Files

Depending on how you installed PowerShell Universal, you will need to uninstall the application files.

### ZIP Installation

If you installed using a provided ZIP file, you can simply stop the PowerShell Universal process or service and delete the folder you extracted to.

### MSI Installation

If you installed with the Windows MSI, uninstall the application from Add\Remove Programs.

### Module Installation

The Universal module installs the application files to the following locations by default.

#### Windows

* `%ProgramData%\PowerShellUniversal`

#### Linux and Mac OS

* `%HOME%/.PowerShellUniversal`

## Configuration Files

Configuration files are stored in the repository folder. Once you have removed the application files, you can delete the configuration files. They are stored in the following locations by default:

### Windows

* `%ProgramData%\PowerShellUniversal`
* `%ProgramData%\UniversalAutomation`

### Linux

* `%HOME%/.PowerShellUniversal/`

### Mac OS

* `%HOME%/.PowerShellUniversal/`

### Desktop

* `%AppData%\PowerShellUniversal`

## Database

Removing the database depends on the database type used.

### SQLite

SQLite databases are stored in a single file on the file system.

#### Windows

* `%ProgramData%\PowerShellUniversal\database.db`

#### Linux and Mac OS

* `%HOME%/.PowerShellUniversal/database.db`

### PostgreSQL and SQL

PostgreSQL and SQL databases are stored on your SQL server and will require you to manually remove the database.

## IIS

You need to remove the IIS App Pool and Website when removing PowerShell Universal. Note that App Pools can be shared amongst websites and caution should be taken when doing so.
