---
description: Installation instructions for PowerShell Universal.
---

# Installation

## Getting Started

{% embed url="https://youtu.be/ISoZbY9YPvo" %}

## PowerShell Module

You can use the PowerShell Universal PowerShell module to install the Universal server. To install the module, use `Install-Module`.

```
Install-Module Universal
```

To install the Universal server, you can use `Install-PSUServer`.

```
Install-PSUServer -LatestVersion
```

If you run this command on Windows, a Windows service will be created and started on your machine. If you run this command on Linux, a systemd service will be created and started. If you run this command on Mac OS, the PowerShell Universal server will be downloaded and extracted. 

## Chocolatey Package (Windows)

You can install PowerShell Universal using the [Chocolatey package](https://chocolatey.org/packages/powershelluniversal). The package runs the MSI install. It will install Universal as a service and open a web browser after the install.

You can login with the "admin" user and any password.

```
choco install powershelluniversal
```

## Winget (Windows)

You can install PowerShell Universal using Winget. It will run the MSI and install as a service.

```
winget install ironmansoftware.powershelluniversal
```

You can also specify the `--silent` flag to prevent the installer from showing and the web browser from opening at the end of the install.

```
winget install ironmansoftware.powershelluniversal --silent
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

You can use the following command line on Linux to install and start PowerShell Universal. 

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

The MSI install will create a PowerShell Universal service and open the admin console after installation.

## Next Steps

At this point, Universal is up and running. Please consult other sections in this documentation for instructions on how to configure, secure, and start using PowerShell Universal. Happy Scripting!
