---
description: Describes how to set application settings and a definition of the settings.
---

# Settings

Application settings can be found within the `appsettings.json` file within the installation directory. This file defines various settings you can apply to Universal. Although you can edit this file directly, it's recommended that you use one of the following methods to persist settings as the `appsettings.json` file in the installation directory will be overridden on upgrades. 

## ProgramData AppSettings.json

You can create an appsettings.json file within the `$Env:ProgramData\PowerShellUniversal` folder. You can use a subset of the settings from within the `appsettings.json` file. For example, if you wanted to override the JWT settings, you could have an `appsettings.json` file like this. 

```text
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

## Setting Descriptions

**Kestrel / Endpoints** 

The Kestrel endpoints section allows you to configure the web server. This settings are not used when hosting in IIS. In this section you can configure options like HTTPS and the port that Universal is listening on. 

Kestrel is the web server implementation for ASP.NET Core that PowerShell Universal uses. For more information on the configuration options for Kestrel, visit this [Microsoft Documentation page](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1#listenoptionsusehttps). 

**Logging**

The logging options define the level of logging exposed by Universal. The core Universal logging setting Logging / LogLevel / Default can be adjusted to increase the level of logging by the Universal components.

**AllowedHosts**

Configures the hosts that are allowed to make cross-origin resource sharing requests \(CORS\) to the server. 

**Data**

* RepositoryPath - Path to the internal git repository used by Universal
* ConnectionString - Path to the database used by Universal
* GitRemote - Git remote used to sync to Universal
* GitUserName - Git user name used to sync to the GitRemote
* GitPassword - Git password used to sync to the GitRemote

**API**

Url - Sets the external URL used internally by Universal. This is necessary when running Universal from within a reverse proxy like IIS. When using cmdlets like `Get-UAScript` from within a running job, the Universal server needs to determine where the web server. When running within a proxy, it cannot determine this itself. You will want to configure this to point to the name and port of the IIS website in this configuration. 

**Authentication**

Windows - Enables or disables Windows Authentication. This setting only works when hosting in IIS and requires that the IIS website has Windows Authentication enabled and Anonymous Authentication disabled. 

OIDC - OpenID Connect authentication settings. You will need to set enabled to true and then set your OIDC settings within the subsequent parameters. You will automatically be forwarded to the OIDC login page when attempting to visit the website. 

WSFed - WS-Federation authentication settings. To enable WS-Federation, ensure that enabled is set to true. You will need to MetadataAddress and Wtrealm to the values you configured in your WS-Federation service. 

**JWT**

JSON Web Token configuration settings. These settings are used for enforcement and granting of web tokens. You should override the default signing key if you plan to use App Tokens. Read-only App Tokens are granted internally when a job calls the Universal cmdlets. You can also issue Read\Write tokens so that jobs can invoke other jobs or set variables. 

