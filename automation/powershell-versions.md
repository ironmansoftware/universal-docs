# PowerShell Versions

When PSU starts for the first time, it will attempt to automatically detect PowerShell versions that exist on your system. These will be stored within the embedded database. The list of available PowerShell versions will be shown in various places within the UI. 

PowerShell versions are used for jobs and for dashboards. When you create a new job or dashboard, you'll be able to adjust the PowerShell version. This executable will then be used to host each component. This enables you the ability to run Windows PowerShell specific scripts in one process while PowerShell specific scripts in another. 

### Manually Configuring Versions

You can configure versions by navigating to the Settings\General page. There is a table of the current PowerShell versions that are available. You will need to specify a name and path to the PowerShell version. 

## Migration to Environments

As of version 1.4, PowerShell versions have been migrated to [Environments](../config/environments.md). 

