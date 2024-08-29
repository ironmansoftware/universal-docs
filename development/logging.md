---
description: Information about logging in PowerShell Universal.
---

# Logging

## About

PowerShell Universal uses a structured logging framework called Serilog. Serilog allows for multiple logging targets (sinks), log event properties and storage of log event data. By default, PowerShell Universal logs two different log files. The first is the system log. This contains log details about the PowerShell Universal server and is set to verbose by default. The second is the user log. The user log captures information about all the scripts run within PowerShell Universal that are created by the user.

Both log files will be found in `%ProgramData%\PowerShellUniversal`.

## System Logging

System logging is configured via the application settings (appsettings.json) or environment variables. System logs typically contain internal logging that is helpful for determining what is happening within the PowerShell Universal server and not necessarily your scripts.&#x20;

The system log settings are found at the root of appsettings.json.&#x20;

```json
{
    "SystemLogPath": "%ProgramData%\\PowerShellUniversal",
    "SystemLogLevel": "Information"
}
```

System log path can contain environment variables. Valid log levels include:&#x20;

* Verbose
* Debug
* Information
* Warning
* Error

We recommend running at Information or above in production environments and only moving below those levels when debugging issues.&#x20;

## Configuration

Logging configuration can be changed within the Settings \ Logging page.

### Targets

PowerShell Universal offers five built in logging targets.

* File
* Database
* TCP
* HTTP
* PowerShell

Each target has its own set of properties. For example, files will have a file path property.

#### Scope

Each target can be configured to capture a specific set of log events based on what is generating them. These include:

* Scope - System or user log messages
* Feature - The feature generating the log message (e.g. API)
* Resource - A specific resource generating the log (e.g. Script1.ps1)

If feature or resource are not specified, then the log target will receive all messages for the scope. For example, if you defined a target with a User scope and an API feature, then it would log all API requests.

#### Level

Log levels define which messages to log based on the level of the log messages. For example, a logging target configured to the Information level will receive log messages from Information through Error but will not log debug or verbose messages.

### PowerShell Target

The PowerShell logging target can be used to create a custom logger with a PowerShell script block to receive the messages. The script block should have two parameters. The first is the log event object produced by Serilog and the second is the rendered message string.

```powershell
New-PSULoggingTarget -Type 'PowerShell' -Level 'Information' -Scope User -Feature API -ScriptBlock {
    param($LogEvent, $Message) 
    
    $Message | Out-File C:\logs\log.txt
}
```

Consider performance when using the PowerShell target as PowerShell will be run for each log message. A logging runspace pool is used to provided multithreaded logging for PowerShell targets.

Do not log within your PowerShell target using Write-PSULog.

## Write-PSULog

You can use the `Write-PSULog` cmdlet to write to logs from within your scripts. The cmdlet automatically sets the User scope and you can choose to provide a feature, resource and message.

```powershell
Write-PSULog -Feature 'MyFeature' -Message 'MyMessage'
```

## Viewing Logs

You can view logs by visiting Platform \ Logging. The log viewer will display all log messages by default. You can use the sorting and filtering options to select particular levels, features and resources to view the logs for.

The search bar will search for log messages containing the search string.

<figure><img src="../.gitbook/assets/image (115).png" alt=""><figcaption><p>Log VIewer</p></figcaption></figure>

## Example: ELK Stack

You can use the TCP logging target to store and parse log messages in ELK stack. For the purpose of this example, we will use the [docker-elk repository](https://github.com/deviantony/docker-elk).

Clone the docker-elk repository and run the following commands in the repository.

```
docker-compose up setup
docker-compose up
```

Once run, you will have ELK stack running. You can visit the web console by navigating to `http://localhost:5601`.

The default username is elastic and the password is changeme.

In PowerShell Universal, you will want to create a logging target and send TCP events to `tcp://localhost:50000`.

```powershell
New-PSULoggingTarget -Type "TCP" -Level "Verbose" -Properties @{
    hostName = 'tcp://localhost'
    port     = '50000'
} -Scope "User"
```

The above configuration will send all User scope log messages to Logstack with the TCP connection. Underneath the Observability section in the console, navigate to the Logs \ Stream page.

<figure><img src="../.gitbook/assets/image (580).png" alt=""><figcaption></figcaption></figure>

From here you will be able to search and view log messages from Universal.

<figure><img src="../.gitbook/assets/image (581).png" alt=""><figcaption></figcaption></figure>
