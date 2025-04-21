---
description: Learn how to revert to a downgrade level of PowerShell Universal.
---

# Downgrade

In some scenarios it may be required to roll back the version of PowerShell Universal. This could be due to a feature change or bug that affects the system in a way too impactful to continue with the version. We [always recommend](upgrading.md) validating a version in a development or quality assurance environment before upgrading in production to avoid having to perform a downgrade. &#x20;

{% hint style="danger" %}
Downgrading can be complicated and error prone. We recommend restoring from a backup or snapshot instead of downgrading.
{% endhint %}

## Configuration Files

Downgrading the configuration files will require removing or altering the `.universal` repository files to remove or rename new parameters. New cmdlets will be ignored by PowerShell Universal. If a cmdlet was renamed, it may have to be updated as well. You will need to refer to the [changelog ](../changelog.md)to see which cmdlets have changed in each version.

Major versions may include breaking changes. Minor versions may have additional cmdlets or parameters but will not have any breaking changes.&#x20;

You can find information about each configuration file in the [Repository page](../config/repository.md).&#x20;

It is much easier to restore from a backup of the configuration files before the upgrade rather than manually updating files.&#x20;

## Database

Restoring the database to a previous version requires downgrading the schema. This can be accomplished with [PSU CLI](../config/psucli.md). Using the `schema` command, you will be able to select the down-level version.&#x20;

{% hint style="danger" %}
Downgrading the database schema can be a destructive operation. You may remove tables and columns that contain data. Always backup a database before performing these operations.
{% endhint %}

Below is an example of downgrading the schema of a SQLite database to version 5.3.0. You will need to stop the PowerShell Universal services before doing so.&#x20;

{% code overflow="wrap" %}
```powershell
.\psu.exe schema --target-version '5.3.0' --connection-string "Data Source=C:\ProgramData\UniversalAutomation\database.db" --database-type "SQLite"
```
{% endcode %}

You can downgrade a nightly build version of the database to a stable version of the database to allow for an upgrade to the stable build of the target version. You will lose any data found in new columns or tables.&#x20;

## Application Files

Downgrading the application files is typically a simple process and depends on how you installed the product. You will need to perform the configuration file and database downgrades before performing the application downgrade.&#x20;

### MSI

To downgrade an MSI installation, you will need to first uninstall the current version. PowerShell Universal will not allow you to run a downgrade. After the uninstall is complete, perform an installation of the target version.&#x20;

If you have configured a service account, you will need to set the service account again after install. This will require the service account credentials.

### ZIP

To downgrade a ZIP installation, simply delete the PowerShell Universal application files. Once the directory is clear unzip the target version's ZIP into the installation directory. Ensure that you run `Get-ChildItem -Recurse | Unblock-File` after doing so.&#x20;

### IIS

Similar to the ZIP installation, remove the old version's files and unzip and unblock the target version's files. Ensure that the web site and App Pool are stopped before attempting so.&#x20;
