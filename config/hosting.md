# Hosting

You can host PowerShell Universal as a Windows Service, in IIS, as a Azure Web App or just as a stand alone application. If you are running on Windows, we suggest either a Windows Service or IIS. 

## Hosting as a Windows Service 

To host as a Windows Service, you can download and install the PowerShell Universal MSI. The MSI will automatically install the PowerShell Universal service and start it. Jobs will run under the system account by default but you can configure the service to run under another account after installation. 

After the MSI has finished setup, your default web browser will open to http://localhost:5000 for login. The default login credentials are set to Admin and any password. 

## Hosting in IIS 

To host in IIS, you will need to download the ZIP of PowerShell Universal. The ZIP contains all the same files as the MSI but requires manually installation. 

You will also need to install the [ASP.NET Core Hosting Bundle 3.1](https://dotnet.microsoft.com/download/dotnet-core/thank-you/runtime-aspnetcore-3.1.3-windows-hosting-bundle-installer). 

You will need the following IIS features enabled

* Web Sockets

Now that you have the prerequisities installed, you can configure your web site. Create a new AppPool within IIS for Universal. The AppPool identity will be the default user that jobs and dashboards will run under. You will need to ensure that the AppPool identity has access to the location of the Universal binary files. 

Set the .NETCLR Version to No Managed Code. 

Now, create a website that utitlizies the AppPool you just configured. Within the Universal ZIP, you will find an web.config file. Update the path of the installation directory of Universal. 

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

The settings within the Universal web.config can be adjusted as you see fit. Below you will find a description of each setting. 

### ForwardWindowsAuthToken 

This setting is used for Windows Authentication. If you wish to use Windows Authentication with IIS, ensure that you disable Anonymous Authentication and enable Windows Authentication within your IIS site and then set this setting to true. 

### StdoutLogEnabled and StdoutLogFile

This setting is used for debugging start up issues with your Universal setup. It's recommended to enable this when first configuring IIS integration. You can disable it once everything is configure. You need to ensure that your AppPool identity has write access to the StdOutLogFile location. 

### HostingModel

The hosting model sets how the Universal server will run. When set to InProcess, the Universal Server will run from within the IIS agent. This provides better performance that using OutOfProcess hosting. InProcess hosting does not work with StdOutLogEnabled. It's recommedned to use OutOfProcess hosting while configuring Universal and then enabling InProcess when your agent is running. 

## Hosting Manually

You can also host the Universal server as a stand alone application. Simply run the `Universal.Server.exe` from the binary directory to start the web server. 

