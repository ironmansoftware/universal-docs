---
description: Information about logging in PowerShell Universal.
---

# Logging

## Admin Console

Logging levels can be changed within the Settings \ General \ Diagnostics page.&#x20;

The Log Level setting configures PowerShell Universal logging settings. The Microsoft Log Level setting controls more low-level components within the web server. This is useful for debugging issues with authentication or authorization.&#x20;

![](<../.gitbook/assets/image (362).png>)

Clicking Download Logs will provide a zip archive of all the log files in the log directory on the server.&#x20;

## appsettings.json

Logging is controlled back the [application settings](../config/settings.md). By default, logging is enabled for the Information level and above. Also by default, logs are written to the `%ProgramData%\PowerShellUniversal` folder.

### Changing the Logging Level

To adjust the logging level, change the values in the `appsettings.json` file in the Logging  LogLevel section.

For example, to enable debug logging, set all the levels to debug.

```javascript
"Logging": {
    "Path":"%HOME%/.PowerShellUniversal/log.txt",
    "LogLevel": {
    "Default": "Debug",
    "Microsoft": "Debug",
    "Microsoft.Hosting.Lifetime": "Debug"
    }
  },
```

This setting can also be set using environment variables. These values need to be set before starting the Universal server.

```
$Env:Logging__LogLevel__Default = "Debug"
```

### Changing the Logging Path

To adjust the logging path, change the values in the `appsettings.json` file in the Logging  Path section.

```javascript
  "Logging": {
      "Path":"C:\log.txt",
      "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
      }
    },
```

This setting can also be set using environment variables. These values need to be set before starting the Universal server.

```
$Env:Logging__Path = "C:\log.txt"
```

## Logging in IIS

In addition to the logs produced by the Universal server, you can also retrieve log files produced by IIS. Log files for IIS are configured in the `web.config` file that is provided by Universal. By default, these logs are in the base website directory's log folder.

You can disable these logs by setting `stdoutLogEnabled` to false.

```markup
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\Universal.Server" arguments="" forwardWindowsAuthToken="false" stdoutLogEnabled="true" stdoutLogFile=".\logs\log" hostingModel="OutOfProcess" />
  </system.webServer>
</configuration>
<!--ProjectGuid: 588ACF2E-9AE5-4DF1-BC42-BCE16A4C4EDE-->
```

## Event Logs

Universal will create event log entries for Warning and Error logs. These logs are typically produced by unhandled exceptions that crash the process or by errors thrown by the Universal web host.

These logs can be found by looking for Warning and Error level messages produced by the .NET Runtime source.

![](<../.gitbook/assets/image (161).png>)

## Common Logging Scenarios

### Out of Process Startup Failure in IIS

This error is produced when the IIS server fails to start Universal. The problem can be diagnosed by looking in the [stdout logs produced by IIS](logging.md#logging-in-iis) and the [logs produced by Universal](logging.md).

It may also be helpful to run the Universal server outside of IIS to validate that the server can properly run Universal.

### Did not receive port from client process

Universal uses gRPC to communicate with external PowerShell processes that are started by the system. These processes run jobs, dashboards and the API server. This error indicates that the PowerShell process did not start correctly.

To diagnosis this issue, [enable Debug logging](logging.md#changing-the-logging-level) for the Universal server. Debug logging will record the stdout from the PowerShell process to capture any startup errors that may be occurring in the process.
