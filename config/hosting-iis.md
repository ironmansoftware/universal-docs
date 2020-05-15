# Hosting with IIS

## Hosting in IIS

PowerShell Universal supports being hosted in IIS \(Internet Information Services \(IIS\) for Windows® Server\). Please note that a series of host prerequisites and specific configuration steps are required to facilitate running PowerShell universal on IIS. Please review each section carefully as IIS requires many specific configuration settings applied to work with modern .NET Core applications such as PowerShell Universal.

{% embed url="https://www.youtube.com/watch?v=jKdGPAn4WzA&feature=youtu.be" %}

## Step 1 : Preparing the IIS Host

The following components are required in order to host PowerShell Universal on IIS. 

* [Internet Information Services \(IIS\) Version 10.0](https://docs.microsoft.com/en-us/iis/get-started/whats-new-in-iis-10-version-1709/new-features-introduced-in-iis-10-1709)
* [ASP.NET Core Hosting Bundle 3.1](https://dotnet.microsoft.com/download/dotnet-core/thank-you/runtime-aspnetcore-3.1.3-windows-hosting-bundle-installer). 

First Make sure to enable is IIS feature on Windows Server and then install the ASP.NET Core hosting bundle.

**NOTE**: IIS often requires a host reboot after installing the .NET Core Hosting bundle! It is strongly recommended that you REBOOT the IIS host after installing the .NET Core Hosting bundle.

The following Windows Server IIS features are also required to be enabled on the IIS Host:

| Feature Display Name | Requirement | Installation Script |
| :--- | :--- | :--- |
| WebSocket Protocol | Required to run PowerShell Universal | `Install-WindowsFeature Web-WebSockets` |
| Windows Authentication | Required for using Windows Authentication | `Install-WindowsFeature  Web-Windows-Auth` |

Once these prerequisites are met, you are ready to begin configuration of PowerShell Universal on IIS.

## Step 2 : Download PowerShell Universal

Download the Latest copy of PowerShell Universal. You will need to download the **ZIP** Archive version of PowerShell Universal. This archive is specifically built for those wishing to configuration PowerShell Universal for IIS or other third party web servers. Extract the contents of the Zip to the intended web host folder location on your IIS Host. 

{% hint style="warning" %}
This location is very important and will be referenced throughout this document. Most importantly this location must be accessible by the Identity used by the  IIS Application Pool.
{% endhint %}

## Step 3 : IIS Application Pool Configuration

Now that our Host is ready and we have downloaded PowerShell Universal, we can begin configuring IIS.

The First step in the IIS configuration process is to create a new Application Pool in IIS. Before we begin the configuration we should ensure that we select a valid identity for the IIS Application Pool.

### 3.1 : Choosing an App Pool Identity

The Application Pool Identity is very important for PowerShell Universal as this will be the "default user" that that jobs and dashboards will run under. It will also be the user that will perform read/write operations to the Universal Automation database, and will be used by IIS to read the web content directory and execute the application.

**Identity Requirements**

* [ ] Full Read/Write access the PowerShell Universal Application Folder we extracted in **Step 2**
* [ ] Full Read/Write access to the PowerShell Universal Database : Default: _C:\ProgramData\Universal Automation_

{% hint style="info" %}
The Default Database location can be customized via the PowerShell Universal `appsettings.json` file if desired.
{% endhint %}

Once we have selected a valid identity we are ready to create the Application Pool in IIS.

### 3.2 : Creating the New IIS Application Pool

Now that we have chosen an App Pool identity that has read/write access to the PowerShell Universal Application and Database folders we can create the Application Pool in IIS.

* In IIs Manager, Choose the option to **Add Application Pool...**  
  * **Name:** Use any Name you would like for the Application Pool
  * **.NET CLR Version**: No managed code
  * ![Application Pool Basic Settings](../.gitbook/assets/image%20%2827%29.png)
  * Click **OK** create the Application Pool.

### 3.3 : Configure the "Advanced Settings" of the IIS Application Pool

Now that the Application Pool has been created, we will need to configure the **Advanced Settings**

* Open the "**Advanced Settings"** for the Application Pool and apply the following Configurations:
  * **General / Enable 32-Bit Applications**: False
  * **Process Model / Identity**: Use the Identity we selected for our Application Pool in the "Choosing an App Pool Identity" section above. 
  * **Process Model / Load User Profile**: True

Once the Advanced Settings have been applied, our Application Pool is ready, our next step will be to configure the IIS Web Site that will utilize this Application Pool.

## Step 4 : IIS Web Site Configuration

### 4.1 : Prepping the web.config for our Website

Now that we have a valid Application Pool we need to create an IIS website to expose the application. Before we do this we will want to review the PowerShell Universal `web.config` file for our website. Within the extracted PowerShell Universal Application folder, we will find a web.config file. This configuration file has been specifically designed for IIS and has a number of configurations we need to review prior to creating the IIS Website.

Most Importantly we will need to update "**processPath**" argument value of this configuration file. This value will provide IIS with the exact path of the application binary so that it can properly launch the application.

* Open the web.config file in the PowerShell Universal Application Folder
  * Locate the **&lt;aspNetCore** **processPath** section of the configuration file
  * Update the arguments=**"PATH"** value to be the exact location of the Universal.Server.dll path.
  * Save the file to apply the configuration

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

{% hint style="info" %}
There are a variety of additional configurations in this file. We'll be reviewing these in more detail in the "Advanced Configuration" Section but you can refer to the "**Additional web.config configurations**" on this page for more details
{% endhint %}

### 

### 4.2 : Creating the IIS Website for IIS

Now that an Application Pool has been created for PowerShell Universal with a valid Identity and we have configured the web.config file,  we are finally ready to create the IIS Website. The Website component of IIS loads the application artifacts and exposes the application on the configured web endpoint.

1. In the IIS Manager: Click "Add Website.."
2. Configure the new website options :
   * **Site Name**: Use any name you would like, ex: `PowerShell Universal.`
   * **Application Pool**: **DO NOT** use the _DefaultAppPool_ - **Select** the Application Pool we created in our previous step.
   * **Physical Path**: This must be the physical path to the PowerShell Universal Content we extracted from our download .zip file.  **NOTE**: The AppPool identity must have access to the location.
   * **Binding Settings**: Note, for initial configuration is suggested to use the base defaults, we'll update these later in our advanced configuration

     * Type http - For Initial Configuration
     * IP Address: All Unassigned
     * Port: 80
     * Host Name: Name of the Host

## Step 5 : Starting Website

At this point, all the required configurations should be in place, and the IIS website hosting PowerShell Universal should be up and running. With a web browser - browse to the configured website location to validate that PowerShell Universal has started. From here you can follow the "Getting Started" guide to validate base functionality. Once you are sure that the Application is working properly with a Basic IIS configuration you can proceed to the "Advanced Configuration" to secure and finalize your desired IIS Configuration.

{% hint style="info" %}
You are are still experiencing issues with the basic IIS Configuration try checking the "Logs" path specified in the web.config for common issues. If you are still experiencing issues reach out on the forums or support for assistance.
{% endhint %}

## Additional web.config configurations

The settings within the Universal web.config can be adjusted as you see fit. Below you will find a description of each setting.

### ForwardWindowsAuthToken

This setting is used for Windows Authentication. If you wish to use Windows Authentication with IIS, ensure that you disable Anonymous Authentication and enable Windows Authentication within your IIS site and then set this setting to true.

### StdoutLogEnabled and StdoutLogFile

This setting is used for debugging start up issues with your Universal setup. It's recommended to enable this when first configuring IIS integration. You can disable it once everything is configured. You need to ensure that your AppPool identity has write access to the StdOutLogFile location.

### HostingModel

The hosting model sets how the Universal server will run. When set to InProcess, the Universal Server will run from within the IIS agent. This provides better performance than using OutOfProcess hosting. InProcess hosting does not work with StdOutLogEnabled. It's recommended to use OutOfProcess hosting only while configuring Universal and, InProcess when your configuration steps have been completed.

