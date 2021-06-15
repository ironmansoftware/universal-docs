---
description: Describes how to set application settings and a definition of the settings.
---

# Settings

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

```text
$Env:Authentication__OIDC__ClientSecret = "mySecret"
```

Using an environment variable for JWT signing key.

```text
$Env:Jwt__SigningKey = "mySigningKey"
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

| Key | Description |
| :--- | :--- |
| RedirectToHttps | When true, the web server will redirect HTTP requests to HTTPS |

### Application Insights

**Default value**

```javascript
    "ApplicationInsights": {
  "InstrumentationKey": ""
},
```

| Key | Description |
| :--- | :--- |
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

| Key | Description |
| :--- | :--- |
| Path | Path to the log file. |
| RetainedFileCountLimit | The number of log files to retain. A new log file will be created each day. |
| LogLevel | The log levels for various portions for the Universal server. You can set values such as Debug, Information, Warning and Error. |

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

Configures the hosts that are allowed to make cross-origin resource sharing requests \(CORS\) to the server. To allow multiple hosts, separate each host by a semicolon.

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
  "ConfigurationScript": ""
},
```

| Key | Description |
| :--- | :--- |
| RepositoryPath | Path to the storage location of the configuration files used by Universal. |
| ConnectionString | Path to the database used by Universal. |
| GitRemote | Git remote used to sync to Universal. |
| GitBranch | Git branch to checkout when syncing to Universal. |
| GitUserName | Git user name used to sync to the GitRemote. When using a PAT, this can be any value. |
| GitPassword | The Git user password or personal access token used to sync to the GitRemote. |
| ConfigurationScript | Location of a custom configuration script to load. You can return objects like scripts, dashboards and endpoints from this script. |

### **API**

**Default Value**

```javascript
    "Api": {
  "Url": ""
},
```

| Key | Description |
| :--- | :--- |
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

| **Key** | Description |
| :--- | :--- |
| Enabled | Enables or disables [Windows Authentication](../api/security.md#authenticating-with-windows-authentication). |

#### OIDC

OpenID Connect authentication settings.

| Key | Description |
| :--- | :--- |
| Enabled | Whether OIDC is enabled. |
| CallbackPath | The path that the OIDC provider will call back to. |
| ClientID | The configured OIDC client ID. |
| ClientSecret | The configured OIDC client secret. |
| Resource | Resources granted with this OIDC token. |
| Authority | The authority to invoke when authenticating. This is the URL of your OIDC provider. |
| ResponseType | The type of response returned by the provider. This most common value here is `code` |
| SaveTokens | Whether to save the token so it is available to endpoints like dashboards. |
| CorrelationCookieSameSite | [Correlation cookie same settings. ](https://docs.microsoft.com/en-us/aspnet/core/security/samesite?view=aspnetcore-5.0) |
| UseTokenLifetime | If set to true, the cookie life time will be set to the token life time. This overrides the session time out value. |

#### WSFed

WS-Federation authentication settings.

| Key | Description |
| :--- | :--- |
| Enabled | Whether WS-Fed is enabled. |
| MetadataAddress | The metadata address to retrieve information about the WS-Fed instance. |
| Wrealm |  |
| Wreply |  |
| CallbackPath | The path that the OIDC provider will call back to. |
| UseTokenLifetime | If set to true, the cookie life time will be set to the token life time. This overrides the session time out value. |
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

| Key | Description |
| :--- | :--- |
| SigningKey | The signing key for the JWT tokens. |
| Issuer | The issuer that will be included in the token. |
| Audience | The audience that will be included in the token. |

### UniversalDashboard

**Default Value**

```javascript
    "UniversalDashboard": {
  "AssetsFolder": "%ProgramData%\\PowerShellUniversal\\Dashboard"
},
```

| Key | Description |
| :--- | :--- |
| AssetsFolder | The location to store components and frameworks. |

### **HideAdminConsole**

Prevents the service from serving the admin console. This will prevent the admin console from being used by any user, including administrators.

