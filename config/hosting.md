# Hosting

You can host PowerShell Universal as a Windows Service, in IIS, as a Azure Web App or just as a stand alone application. If you are running on Windows, we suggest either a Windows Service or IIS. 

## Hosting as a Windows Service 

To host as a Windows Service, you can download and install the PowerShell Universal MSI. The MSI will automatically install the PowerShell Universal service and start it. Jobs will run under the system account by default but you can configure the service to run under another account after installation. 

After the MSI has finished setup, your default web browser will open to http://localhost:5000 for login. The default login credentials are set to Admin and any password.

## Hosting in IIS 

To host in IIS, you will need to download the ZIP of PowerShell Universal. The ZIP contains all the same files as the MSI but requires manual installation.

Hosting in IIS is fully supported but there are a number of specific configuration options that need to applied in order to host with IIS.

Visit our [IIS Hosting](.\hosting-iis.md) Page for specific IIS Instructions.


## Hosting Manually

You can also host the Universal server as a stand alone application. Simply run the `Universal.Server.exe` from the binary directory to utilize the [Kestrel web server implementation in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1) to start the web server.
