# Hosting

You can host PowerShell Universal as a Windows Service, in IIS, as a Azure Web App or just as a stand alone application. If you are running on Windows, we suggest either a Windows Service or IIS.

## Hosting as a Windows Service

To host as a Windows Service, you can download and install the PowerShell Universal MSI. The MSI will automatically install the PowerShell Universal service and start it. Jobs will run under the system account by default but you can configure the service to run under another account after installation.

After the MSI has finished setup, your default web browser will open to [http://localhost:5000](http://localhost:5000) for login. The default login credentials are set to Admin and any password.

### Configuring a Windows Service Manually

You do not need to use the MSI to configure Universal as a Windows Service. You can also do it manually with the following PowerShell script.

```text
New-Service -Name "PowerShellUniversal" -BinaryPathName "Universal.Server.exe --service" -Description "PowerShell Universal server service." -DisplayName "PowerShell Universal" -StartupType Automatic
Start-Service PowerShellUniversal
```

## Hosting in Azure

You can host PowerShell Universal in Azure as a Linux, Windows or Docker web app. To create a persistent web app, it's easiest to deploy using a standard Azure Web App. 

We have a [GitHub repository that contains a GitHub action workflow](https://github.com/ironmansoftware/universal-azure-actions) for downloading the latest version of PowerShell Universal, updating `appsettings.json` and `web.config` to work with Azure and then deploying to an existing web app. 

## Hosting in IIS

To host in IIS, you will need to download the ZIP of PowerShell Universal. The ZIP contains all the same files as the MSI but requires manual installation.

Hosting in IIS is fully supported but there are a number of specific configuration options that need to applied in order to host with IIS.

Visit our [IIS Hosting](hosting-iis/) Page for specific IIS Instructions.

## Hosting Manually

You can also host the Universal server as a stand alone application. Simply run the `Universal.Server.exe` from the binary directory to utilize the [Kestrel web server implementation in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1) to start the web server.

## Web Server Configuration 

{% hint style="info" %}
This section applies to Universal when it is hosted outside of IIS. 
{% endhint %}

### Setting the Port and Listening Address

You can set the port of the Universal server by modifying the `appsettings.json` file. We recommend that you create an `appsettings.json` file in the [default configuration folder](https://docs.ironmansoftware.com/config/settings).

**Windows** 

`%ProgramData%\PowerShellUniversal`

**Linux** 

`%HOME%/.PowerShellUniversal`

To set the port, change the Kestrel endpoints section of the `appsettings.json`. By default, the configuration is defined to listen on port 5000 and on any address. 

```text
 "Kestrel": {
    "Endpoints": {
      "HTTP": {
        "Url": "http://*:5000"
      }
    }
  },
```

### Configuring HTTPS

To configure HTTPS, you can adjust the `appsettings.json` file to use a particular certificate and port. The below configuration uses the `testCert.pfx` file and `testPassword` and listens on port 5463. 

```text
{
  "Kestrel": {
	"Endpoints": {
	   "HTTP": { "Url": "http://*:5000" },
           "HTTPS": {
              "Url": "https://*:5463",
              "Certificate": {
                  "Path": "testCert.pfx",
                  "Password": "testPassword"
              }
          }
    }
}
```

To configure a certificate in a particular location and store, you can use a configuration such as this. 

```text
"HTTPS": {
  "Url": "https://*443",
  "Certificate": {
    "Subject": "windows-server.ironman.local",
    "Store": "My",
    "Location": "LocalMachine",
    "AllowInvalid": "true"
  }
}
```

Location can be either `CurrentUser` or `LocalMachine`.

For a full set of listening options, you can refer to the [ASP.NET Core Documentation](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1#listenoptionsusehttps).

