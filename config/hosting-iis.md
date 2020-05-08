## Hosting in IIS 

PowerShell Universal supports being hosted in IIS (Internet Information Services (IIS) for Windows® Server). Please note that a series of host prerequisites and specific configuration steps are required to facilitate running PowerShell universal on IIS. 

## Preparing the IIS Host


* [Internet Information Services (IIS) Version 10.0](https://docs.microsoft.com/en-us/iis/get-started/whats-new-in-iis-10-version-1709/new-features-introduced-in-iis-10-1709)
* [ASP.NET Core Hosting Bundle 3.1](https://dotnet.microsoft.com/download/dotnet-core/thank-you/runtime-aspnetcore-3.1.3-windows-hosting-bundle-installer). 

**NOTE**: IIS often requires a host reboot after installing the .NET Core Hosting bundle!

The following Windows Server IIS features are also required to be enabled on the IIS Host:

| Feature Display Name | Requirement | Installation Script |
|----------------------|---------------|---------------------|
| WebSocket Protocol   | Required to run PowerShell Universal | ``Install-WindowsFeature Web-WebSockets`` |
| Windows Authentication |  Required for using Windows Authentication | ``Install-WindowsFeature  Web-Windows-Auth`` |

Once these prerequisites are met, you are ready to begin configuration of PowerShell Universal on IIS.


## Download PowerShell Universal

Download the Latest copy of PowerShell Universel. You will need to download the ZIP of PowerShell Universal. The ZIP contains all the same files as the MSI but requires manual installation. 
Extract the contents of the Zip to the intended web host folder (such as inetpub) location on your IIS Host



## IIS Application Pool Configuration
Now that our Host is ready and we have downloaded PowerShell Universal, we can begin configuring IIS. 

The First step in the configuration process for IIS is to create a new Application Pool in IIS. In this instance, the Application Pool must be configurated to support .NET Core applications. This requires several important configuration options to be set on the application pool.

### Choosing an App Pool Identity

**Important** : The AppPool identity will be the default user that jobs and dashboards will run under. You will need to ensure that the AppPool identity has access to the location of the Universal binary files. 
[More Details on AppPool Identities](https://docs.microsoft.com/en-us/iis/manage/configuring-security/application-pool-identities)

This AppPool identity will be the default user that jobs and dashboards will run under. You will need to ensure that the AppPool identity has access to the location of the Universal binary files.

**NOTE** The Default Database location can be customized via the PowerShell Universal ``appsettings.json`` file if desired. The Application Pool Identity will still need read/write access to this location


### Creating the New IIS Application Pool

Now that we have chosen an App Pool identity that has read/write access to the PowerShell Universal Application Content folder we can create the Application Pool in IIS.

 * Create a new AppPool within IIS for Universal. 
   - **.NET CLR Version**: No managed code
    - **Identity**: Use a Service account with full permissions to extracted location of the PowerShell Universal Zip file we extract previously AND the and the default database location: ``C:\ProgramData\UniversalAutomation``
    - **Advanced Settings / Process Model / LoadUser Profile**: True
    - **Advanced Settings / (General) / Enable 32-Bit Applications**: False


## IIS Web Site Configuration


### Prepping the web.config for our Website

Now that we have a valid Application Pool we need to create an IIS website to expose the application. Before we do this we will want to review the PowerShell Universal ``web.config`` file for our website. Within the PowerShell Universal ZIP contents, you will find a web.config file. This configuration file has been specifically designed for IIS and has a number of configurations we need to review prior to creating the IIS Website.

* **processPath** - Update the path of the installation directory of Universal. 

```text
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="dotnet" arguments="C:\Program Files (x86)\Universal\Universal.Server.dll" forwardWindowsAuthToken="false" stdoutLogEnabled="true" stdoutLogFile=".\logs\log" hostingModel="InProcess"/>
  </system.webServer>
</configuration>
```

### Creating the IIS Website for IIS

Now that an Application Pool has been created for PowerShell Universal with a valid Identity and we have configured the web.config file we are ready to create the IIS Website. The Website component of IIS loads the application artifacts and exposes the application on the configured web endpoint.

1. In the IIS Manager: Click "Add Website.."
2. Configure the new website options :
    * **Site Name**: Use any name you would like, ex: ``PowerShell Universal. ``
    * **Application Pool**: **DO NOT** use the *DefaultAppPool* - **Select** the Application Pool we created in our previous step.
    * **Physical Path**: This must be the physical path to the PowerShell Universal Content we extracted from our download .zip file.  **NOTE**: The AppPool identity must have access to the location.
    * **Binding Settings**: Note, for initial configuration is suggested to use the base defaults, we'll update these later in our advanced configuration
        * Type http - For Initial Configuration
        * IP Address: All Unassigned
        * Port: 80
        * Host Name: Name of the Host


## Additional web.config configurations

The settings within the Universal web.config can be adjusted as you see fit. Below you will find a description of each setting. 

### ForwardWindowsAuthToken 

This setting is used for Windows Authentication. If you wish to use Windows Authentication with IIS, ensure that you disable Anonymous Authentication and enable Windows Authentication within your IIS site and then set this setting to true. 

### StdoutLogEnabled and StdoutLogFile

This setting is used for debugging start up issues with your Universal setup. It's recommended to enable this when first configuring IIS integration. You can disable it once everything is configured. You need to ensure that your AppPool identity has write access to the StdOutLogFile location. 

### HostingModel

The hosting model sets how the Universal server will run. When set to InProcess, the Universal Server will run from within the IIS agent. This provides better performance than using OutOfProcess hosting. InProcess hosting does not work with StdOutLogEnabled. It's recommended to use OutOfProcess hosting only while configuring Universal and, InProcess when your configuration steps have been completed.