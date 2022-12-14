---
description: Describes how to set application settings and a definition of the settings.
---

# App Settings

Application settings can be found within the `appsettings.json` file within the installation directory. This file defines various settings you can apply to Universal. Although you can edit this file directly, it's recommended that you use one of the following methods to persist settings as the `appsettings.json` file in the installation directory will be overridden on upgrades.

{% hint style="info" %}
When installed from the MSI, the installation directory for PowerShell Universal is `${env:ProgramFiles(x86)}\Universal`.
{% endhint %}

## ProgramData AppSettings.json

You can create an appsettings.json file within the `$Env:ProgramData\PowerShellUniversal` folder. You can use a subset of the settings from within the `appsettings.json` file. For example, if you wanted to override the JWT settings, you could have an `appsettings.json` file like this.

```javascript
{
  "Jwt": {  
    "SigningKey": "PleaseUseYourOwnSigningKeyHere",  
    "Issuer": "IronmanSoftware",
    "Audience": "PowerShellUniversal"
  }
}
```

## Environment Variables

You can also set environment variables for your settings. Environment variables should have an underscore between each subset of the `appsettings.json` file. For example, if you want to change the JWT signing key via environment variable, you would set the variable `$Env:Jwt__SigningKey`. If you wanted to set the external API URL, you would set `$Env:Api__Url`.

### Examples

Using an environment variable for the OpenID Connect secret.

```
$Env:Authentication__OIDC__ClientSecret = "mySecret"
```

Using an environment variable for JWT signing key.

```
$Env:Jwt__SigningKey = "mySigningKey"
```

## Command Line&#x20;

You can specify the location of the `appsettings.json` file by using the `--appsettings` command line argument for `Universal.Server.exe` .

```powershell
.\Universal.Server.exe --appsettings C:\appsettings.json
```

## Setting Descriptions

### Kestrel / Endpoints

**Default Value**

```javascript
"Kestrel": {
  "Endpoints": {
    "HTTP": {
      "Url": "http://*:5000"
    }
  },
  "RedirectToHttps": "false"
},
```

The Kestrel endpoints section allows you to configure the web server. This settings are not used when hosting in IIS. In this section you can configure options like HTTPS and the port that Universal is listening on.

Kestrel is the web server implementation for ASP.NET Core that PowerShell Universal uses. For more information on the configuration options for Kestrel, visit this [Microsoft Documentation page](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1#listenoptionsusehttps).

| Key             | Description                                                    |
| --------------- | -------------------------------------------------------------- |
| RedirectToHttps | When true, the web server will redirect HTTP requests to HTTPS |

### Application Insights

**Default value**

```javascript
"ApplicationInsights": {
  "InstrumentationKey": ""
},
```

| Key                | Description                                            |
| ------------------ | ------------------------------------------------------ |
| InstrumentationKey | Sets the instrumentation key for Application Insights. |

### Logging

**Default Value**

```javascript
"Logging": {
  "Path": "%PROGRAMDATA%/PowerShellUniversal/log.txt",
  "RetainedFileCountLimit": 31,
  "LogLevel": {
    "Default": "Information",
    "Microsoft": "Warning",
    "Microsoft.Hosting.Lifetime": "Information"
  }
},
```

The logging options define the level of logging exposed by Universal. The core Universal logging setting Logging / LogLevel / Default can be adjusted to increase the level of logging by the Universal components.

| Key                    | Description                                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Path                   | Path to the log file.                                                                                                           |
| RetainedFileCountLimit | The number of log files to retain. A new log file will be created each day.                                                     |
| LogLevel               | The log levels for various portions for the Universal server. You can set values such as Debug, Information, Warning and Error. |

### AllowedHosts

**Default Value**

```javascript
    "AllowedHosts": "*",
```

The hosts that are allowed to connect to the webserver. Defaults to any host.

### **CorsHosts**

**Default Value**

```javascript
    "CorsHosts": "",
```

Configures the hosts that are allowed to make cross-origin resource sharing requests (CORS) to the server. To allow multiple hosts, separate each host by a semicolon.

```javascript
"CorsHosts" : "https://www.google.com;https://login.microsoftonline.com"
```

### **Data**

**Default Value**

```javascript
"Data": {
  "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
  "ConnectionString": "%ProgramData%\\UniversalAutomation\\database.db",
  "GitRemote": "",
  "GitUserName": "",
  "GitPassword": "", 
  "GitBranch": "",
  "ConfigurationScript": "",
  "Mode": "automatic"
},
```

| Key                 | Description                                                                                                                        |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| RepositoryPath      | Path to the storage location of the configuration files used by Universal.                                                         |
| ConnectionString    | Path to the database used by Universal.                                                                                            |
| GitRemote           | Git remote used to sync to Universal.                                                                                              |
| GitBranch           | Git branch to checkout when syncing to Universal.                                                                                  |
| GitUserName         | Git user name used to sync to the GitRemote. When using a PAT, this can be any value.                                              |
| GitPassword         | The Git user password or personal access token used to sync to the GitRemote.                                                      |
| ConfigurationScript | Location of a custom configuration script to load. You can return objects like scripts, dashboards and endpoints from this script. |
| Mode                | Sets the git mode. It can be either manual or automatic. Defaults to manual.                                                       |

### **API**

**Default Value**

```javascript
"Api": {
  "Url": ""
},
```

| Key | Description                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Url | Sets the external URL used internally by Universal. This is necessary when running Universal from within a reverse proxy like IIS. When using cmdlets like `Get-UAScript` from within a running job, the Universal server needs to determine where the web server. When running within a proxy, it cannot determine this itself. You will want to configure this to point to the name and port of the IIS website in this configuration. |

### **Authentication**

**Default Value**

```javascript
    "Authentication" : {
    "Windows": {
      "Enabled": "false"
    },
    "WSFed": {
      "Enabled": "false",
      "MetadataAddress": "",
      "Wtrealm": "",
      "CallbackPath": "/auth/signin-wsfed",
      "Wreply": "",
      "UseTokenLifetime": true,
      "CorrelationCookieSameSite": ""
    },
    "OIDC": {
      "Enabled": "false",
      "CallbackPath": "/auth/signin-oidc",
      "ClientID": "",
      "ClientSecret": "",
      "Resource": "",
      "Authority": "",
      "ResponseType": "",
      "SaveTokens": "false",
      "CorrelationCookieSameSite": "",
      "UseTokenLifetime": true
    },
    "SessionTimeout": "25"
  },
```

**Windows**

| **Key** | Description                                                                                                  |
| ------- | ------------------------------------------------------------------------------------------------------------ |
| Enabled | Enables or disables [Windows Authentication](../api/security.md#authenticating-with-windows-authentication). |

#### OIDC

OpenID Connect authentication settings.

| Key                       | Description                                                                                                                                 |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Enabled                   | Whether OIDC is enabled.                                                                                                                    |
| CallbackPath              | The path that the OIDC provider will call back to.                                                                                          |
| ClientID                  | The configured OIDC client ID.                                                                                                              |
| ClientSecret              | The configured OIDC client secret.                                                                                                          |
| Resource                  | Resources granted with this OIDC token.                                                                                                     |
| Authority                 | The authority to invoke when authenticating. This is the URL of your OIDC provider.                                                         |
| ResponseType              | The type of response returned by the provider. This most common value here is `code`                                                        |
| SaveTokens                | Whether to save the token so it is available to endpoints like dashboards.                                                                  |
| CorrelationCookieSameSite | [Correlation cookie same settings. ](https://docs.microsoft.com/en-us/aspnet/core/security/samesite?view=aspnetcore-5.0)                    |
| UseTokenLifetime          | If set to true, the cookie life time will be set to the token life time. This overrides the session time out value.                         |
| GetUserInfo               | Returns additional user information for use within roles.ps1 files. You can access the additional information using the $UserInfo variable. |

#### WSFed

WS-Federation authentication settings.

| Key                       | Description                                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Enabled                   | Whether WS-Fed is enabled.                                                                                               |
| MetadataAddress           | The metadata address to retrieve information about the WS-Fed instance.                                                  |
| Wrealm                    |                                                                                                                          |
| Wreply                    |                                                                                                                          |
| CallbackPath              | The path that the OIDC provider will call back to.                                                                       |
| UseTokenLifetime          | If set to true, the cookie life time will be set to the token life time. This overrides the session time out value.      |
| CorrelationCookieSameSite | [Correlation cookie same settings. ](https://docs.microsoft.com/en-us/aspnet/core/security/samesite?view=aspnetcore-5.0) |

### **JWT**

JSON Web Token configuration settings

**Default Value**

```javascript
"Jwt": {  
  "SigningKey": "PleaseUseYourOwnSigningKeyHere",  
  "Issuer": "IronmanSoftware",
  "Audience": "PowerShellUniversal"
},
```

| Key        | Description                                      |
| ---------- | ------------------------------------------------ |
| SigningKey | The signing key for the JWT tokens.              |
| Issuer     | The issuer that will be included in the token.   |
| Audience   | The audience that will be included in the token. |

### Secrets

Options for configuring the default secret vaults.&#x20;

**Default Value**

```json
"Secrets": {
  "SecretStore": {
    "Password": "PSUSecretStore"
  },
  "Database": {
    "EncryptionKey": "=b0ywQA@VOSdr&R7an5g&XK6NVO%s4Tf"
  }
}
```

| Key                      | Description                                                                            |
| ------------------------ | -------------------------------------------------------------------------------------- |
| SecretStore \ Password   | The password for the PSUSecretStore vault. This uses the Microsoft SecretStore module. |
| Database \ EncryptionKey | The AES 256 encryption key used to encrypt secrets stored in the database.             |
|                          |                                                                                        |

### UniversalAutomation

Settings for automation specific features.&#x20;

**Default Value**

```json
"UniversalAutomation": {
    "Queues": [],
    "JobHandshakeTimeout": 5,
    "JobDebugging": false,
    "ContinueJobOnServerStop": false
  }
```

| Key                     | Description                                                                                                                                                    |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Queues                  | Custom queues that this PSU instance is a part of.                                                                                                             |
| JobHandshakeTimeout     | The number of seconds to wait before failing a job after starting the PowerShell process to execute it if the process does not communicate back to the server. |
| JobDebugging            | Whether to generate files in the temporary directory when starting job. This is useful for debugging if jobs are timing out before starting.                   |
| ContinueJobOnServerStop | Whether to continue running a job after the service has stopped. Job progress will fail to be reported but the script will continue to run.                    |

### UniversalDashboard

**Default Value**

```javascript
"UniversalDashboard": {
  "AssetsFolder": "%ProgramData%\\PowerShellUniversal\\Dashboard"
},
```

| Key          | Description                                      |
| ------------ | ------------------------------------------------ |
| AssetsFolder | The location to store components and frameworks. |

### **HideAdminConsole**

Prevents the service from serving the admin console. This will prevent the admin console from being used by any user, including administrators.

### NodeName

The node name option is used to change the name of the PowerShell Universal instance. By default, this is the local computer's name. When using PowerShell Universal in a container, this can become probematic because the name can change whenever the container is restarted.&#x20;

To set a static node name, change this parameter.&#x20;

### Profiling

Enables [profiling](../development/profiling.md) of scripts within PowerShell Universal. This is disabled by default as there is a memory impact when enabling profiling.&#x20;
