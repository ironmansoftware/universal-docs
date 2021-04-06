# About

Universal utilizes an idempotent configuration system to ensure repeatable deployments of instances of the platform. The same cmdlets that are used to call the REST API are used to configure the system. When they are called by the configuration system, they do not call the REST API and just return objects that are then used to configure Universal.

A typical configuration file is just a PS1 file.

```PowerShell
New-PSUDashboard -Name 'Dashboard' -Path 'dashboard.ps1' -Framework 'UniversalDashboard:3.0.0'
```

Using an idempotent configuration system all enables the ability to source control the configuration files used to deploy Universal instances.

## Idempotent Configuration

The configuration files for Universal define the state of the system. Rather than calling a Remove cmdlet to remove an item from the Universal system, you simply remove the New cmdlet call from the established configuration file.

{% hint style="info" %}
You can call the Remove cmdlets to invoke the Universal REST API. The REST API will then synchronize with the configuration files to remove the entity.
{% endhint %}

For example, scripts are added to the system by adding a `New-PSUScript` cmdlet call to the `./universal/scripts.ps1`file.

If you had two scripts, your `scripts.ps1`would look like this.

```PowerShell
New-PSUScript -Name 'Script1.ps1' -Path 'Script1.ps1'
New-PSUScript -Name 'Script2.ps1' -Path 'Script2.ps1'
```

To remove `Script2.ps1`from the system, you would just remove the second line.

```PowerShell
New-PSUScript -Name 'Script2.ps1' -Path 'Script2.ps1'
```

When calling the Universal REST API or by using the Universal admin console, the configuration files will be updated automatically.

## Configuration Files

For each type of entity that is managed within Universal there is a configuration file that will be stored within the `./universal` folder. The `./universal`folder will be managed underneath the `RepositoryFolder` that you define within your `appsettings.json` file.

By default, configuration files will automatically be reloaded when changed. This means that if you make a change to one of the files, Universal will read the file, synchronize to its local database and the platform will have the new setting you defined.

For example, if you wanted to disable telemetry collection, you could change the `./universal/settings.ps1`file. The original settings file may look like this.

```PowerShell
Set-PSUSetting -Telemetry
```

To reconfigure Universal to turn off telemetry collection, you would just remove the `-Telemetry` switch parameter.

```PowerShell
Set-PSUSetting
```

Universal would detect this change and reload internally.

You can disable the automatic reload of the system by specifying the `-DisableAutoReload` switch on `Set-PSUSetting`. Settings will only reload on restart of the system or when a Git synchronization takes place.

## Git Synchronization

Universal provides the ability to automatically synchronization configuration files and other artifacts with a remote git repository. Changes made via the Universal REST API or admin console will result in git commits and then be pushed automatically to the remote. Additionally, changes made in the remote will be pulled and Universal will automatically reload settings internally.

To configure git synchronization, use the `GitRemote`, `GitUserName`, and `GitPassword` settings in the `appsettings.json` file. You will need to restart Universal after making these changes.

To learn more about configuration settings, read the [Settings](settings.md) page.

You can view the status of Git synchronization operations on the `Settings \ General` page within the admin console. Git synchronizations take place one a minute.

