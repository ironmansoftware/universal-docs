# Installation

## Installing Universal

1. [Download the Universal Installer](https://ironmansoftware.com/downloads/)
2. Run the MSI as an Administrator as it installs a service.
3. After the installation has completed, "PowerShell Universal" automatically starts and is ready to use.
4. Using a supported web browser, navigate to `http://localhost:5000` and login with the username "Admin" with any password.

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

Our docker image is available on [Docker Hub](https://hub.docker.com/r/ironmansoftware/universal). You can start it by pulling and then running with the default port bound. 

```text
docker pull ironmansoftware/universal
docker run --name 'PSU' -it -p 5000:5000 ironmansoftware/universal 
```

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

