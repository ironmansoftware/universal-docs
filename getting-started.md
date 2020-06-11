# Getting Started

## Installing Universal

1. [Download the Universal Installer](https://ironmansoftware.com/downloads/)
2. Run the MSI as an Administrator. \(**Note**: You may have to launch the installer from a command prompt as an administrator.\)
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

## Next Steps

At this point, Universal is up and running. Please consult other sections in this documentation for instructions on how to configure, secure, and start using PowerShell Universal. Happy Scripting!

