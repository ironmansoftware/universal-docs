---
description: Installation instructions for PowerShell Universal.
---

# Installation

{% hint style="info" %}
We recommend installing the [PowerShell Universal Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=ironmansoftware.powershell-universal). The extension will automatically download Universal for development purposes. 
{% endhint %}

## Chocolatey Package

You can install PowerShell Universal using the [Chocolatey package](https://chocolatey.org/packages/powershelluniversal). The package runs the MSI install. It will install Universal as a service and open a web browser after the install. 

You can login with the "admin" user and any password.

```text
choco install powershelluniversal
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

On Linux, start the process `Universal.Server`. You may need to `chmod +x` the file if it does not start.  

### Docker

See the [Docker page](docker.md#installation).

## MSI Install

{% hint style="info" %}
This section covers a pre-release version of Universal. You can download nightly builds from our [Downloads page](https://ironmansoftware.com/downloads).
{% endhint %}

The MSI install will create a PowerShell Universal service and open the admin console after installation. 

### Properties

#### SUPPRESSBROWSER

Setting the SUPPRESBROWSER MSI property to true will prevent the browser from opening after installation. 

## Next Steps

At this point, Universal is up and running. Please consult other sections in this documentation for instructions on how to configure, secure, and start using PowerShell Universal. Happy Scripting!

