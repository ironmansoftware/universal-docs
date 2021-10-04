---
description: Installation instructions for PowerShell Universal.
---

# Installation

## Getting Started

{% embed url="https://youtu.be/ISoZbY9YPvo" caption="" %}

## PowerShell Module

You can use the PowerShell Universal PowerShell module to install the Universal server. To install the module, use `Install-Module`.

```text
Install-Module Universal
```

To install the Universal server, you can use `Install-PSUServer`.

```text
Install-PSUServer -LatestVersion
```

You can configure the path that the server is stored in by using the `-Path` parameter.

```text
Install-PSUServer -Path (Join-Path $Env:AppData "PSU")
```

You can add the PSU server to the PATH environment variable by use the `-AddToPath` parameter.

```text
Install-PSUServer -AddToPath
```

Once the server has been installed, you can use `Start-PSUServer` to start it.

```text
Start-PSUServer -Port 8080
```

You can specify the path to the executable using the `-ExecutablePath` parameter. If you have set the location of the server to `-AddToPath` with `Install-PSUServer`, `Start-PSUServer` should find the executable automatically.

```text
Start-PSUServer -Port 8080 -ExecutablePath (Join-Path $MyPath "Universal.Server.exe")
```

## Chocolatey Package \(Windows\)

You can install PowerShell Universal using the [Chocolatey package](https://chocolatey.org/packages/powershelluniversal). The package runs the MSI install. It will install Universal as a service and open a web browser after the install.

You can login with the "admin" user and any password.

```text
choco install powershelluniversal
```

## Winget \(Windows\)

You can install PowerShell Universal using Winget. It will run the MSI and install as a service.

```text
winget install ironmansoftware.powershelluniversal
```

You can also specify the `--silent` flag to prevent the installer from showing and the web browser from opening at the end of the install.

```text
winget install ironmansoftware.powershelluniversal --silent
```

## ZIP Install

You can also download the ZIP from our [Downloads page](https://ironmansoftware.com/downloads/) if you would like to xcopy deploy the files on Windows or Linux.

### Windows

You can start Universal by unzipping the contents, unblocking the files and then executing `Universal.Server.exe`.

```text
Expand-Archive -Path .\Universal.zip -DestinationPath .\Universal
Get-ChildItem .\Universal -Recurse | Unblock-File
Start-Process .\Universal\Universal.Server.exe
```

### Linux

You can use the following command line on Linux to install and start PowerShell Universal. 

```text
 wget https://imsreleases.blob.core.windows.net/universal/production/2.0.0/Universal.linux-x64.2.0.0.zip
 sudo apt install unzip 
 unzip Universal.linux-x64.2.0.0.zip -d PSU
 chmod +x ./PSU/Universal.Server
 ./PSU/Universal.Server
```

### Docker

See the [Docker page](docker.md#installation).

## MSI Install \(Windows\)

The MSI install will create a PowerShell Universal service and open the admin console after installation.

## Next Steps

At this point, Universal is up and running. Please consult other sections in this documentation for instructions on how to configure, secure, and start using PowerShell Universal. Happy Scripting!

