---
description: Installation instructions for PowerShell Universal.
---

# Installation

## PowerShell Module

You can use the PowerShell Universal PowerShell module to install the Universal server. To install the module, use `Install-Module`.

```
Install-Module Universal
```

To install the Universal server, you can use `Install-PSUServer`.

```
Install-PSUServer -LatestVersion
```

If you run this command on Windows, a Windows service will be created and started on your machine. If you run this command on Linux, a systemd service will be created and started. If you run this command on Mac OS, the PowerShell Universal server will be downloaded and extracted.&#x20;

## Chocolatey Package (Windows)

{% hint style="warning" %}
Chocolatey packages for PowerShell Universal are usually available within a week of release but will not be available the day of a release.&#x20;
{% endhint %}

You can install PowerShell Universal using the [Chocolatey package](https://chocolatey.org/packages/powershelluniversal). The package runs the MSI install. It will install Universal as a service and open a web browser after the install.

You can login with the "admin" user and any password.

```
choco install powershelluniversal
```



## ZIP Install

You can also download the ZIP from our [Downloads page](https://ironmansoftware.com/downloads/) if you would like to xcopy deploy the files on Windows or Linux.

### Windows

You can start Universal by unzipping the contents, unblocking the files and then executing `Universal.Server.exe`.

```
Expand-Archive -Path .\Universal.zip -DestinationPath .\Universal
Get-ChildItem .\Universal -Recurse | Unblock-File
Start-Process .\Universal\Universal.Server.exe
```

### Linux

You can use the following command line on Linux to install and start PowerShell Universal.&#x20;

```
 wget https://imsreleases.blob.core.windows.net/universal/production/2.0.0/Universal.linux-x64.2.0.0.zip
 sudo apt install unzip 
 unzip Universal.linux-x64.2.0.0.zip -d PSU
 chmod +x ./PSU/Universal.Server
 ./PSU/Universal.Server
```

### Docker

See the [Docker page](docker.md#installation).

## MSI Install (Windows)

The MSI install will create a PowerShell Universal service. By default, PowerShell Universal will be listening on port 5000. You will be able to navigate to `http://localhost:5000` and login with `admin` and any password.

MSI downloads are available on our [download page](https://ironmansoftware.com/downloads).&#x20;

### MSI Parameters

The following table contains the parameters you can specify if running `msiexec` against our MSI install for automation purposes.&#x20;

| Parameter              | Description                                                 | Default Value                                 |
| ---------------------- | ----------------------------------------------------------- | --------------------------------------------- |
| INSTALLFOLDER          | The installation folder for PowerShell Universal            | %ProgramFiles(x86)%\Universal                 |
| TCPPORT                | The TCP port the HTTP server will be listening on.          | 5000                                          |
| REPOFOLDER             | The repository folder to save the configuration files to.   | %ProgramData%\UniversalAutomation\Repository  |
| CONNECTIONSTRING       | The LiteDB or SQL connection string.                        | %ProgramData%\UniversalAutomation\database.db |
| DATABASETYPE           | LiteDB or SQL                                               | LiteDB                                        |
| STARTSERVICE           | Whether to start the service after install (0 or 1)         | 1                                             |
| SERVICEACCOUNT         | The service account to set for the Windows service          | None                                          |
| SERVICEACCOUNTPASSWORD | The service account password to set for the Windows Service | None                                          |

## IIS Install

Please visit the [IIS hosting documentation](../config/hosting/hosting-iis.md) for information on how to configure PowerShell Universal as an IIS website.&#x20;

## Next Steps

At this point, Universal is up and running. You can navigate to the admin console by visiting `http://localhost:5000` by default. The default user name is admin with any password.&#x20;
