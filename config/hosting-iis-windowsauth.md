# IIS hosting and Windows Authentication 

## Host Preparation

1. Ensure the following IIS Features are installed on the host:

  | Feature Display Name | Feature Name | Feature Path | Installation Script |
  |----------------------|--------------|--------------|---------------------|
  | WebSocket Protocol   |  Web-WebSockets | Web Server (IIS) / Web Server / Common HTTP Feature / Application Development | ``Install-WindowsFeature Web-WebSockets`` |
  | Windows Authentication |  Web-Windows-Auth | Web Server (IIS) / Web Server / Common HTTP Feature / Security | ``Install-WindowsFeature  Web-Windows-Auth`` |

2. Install Windows Hosting Bundle for 3.1.3 - https://dotnet.microsoft.com/download/dotnet-core/thank-you/runtime-aspnetcore-3.1.3-windows-hosting-bundle-installer
3. Restart the Host (IIS Requirement)
4. Install PowerShell Universal
5. Stop and Disable the PowerShell Universal Windows Service
6. Ensure "AspNetCoreModuleV2" is listed as a Module on your IIS server instance.

## IIS Configuration

1. Create a New Application Pool:
    - **.NET CLR Version**: No managed code
    - **Identity**: Use a Service account with full permissions to the application files ``C:\Program Files (x86)\Universal`` and the database files: ``C:\ProgramData\UniversalAutomation``
    - **Advanced Settings / Process Model / LoadUser Profile**: True
    - **Advanced Settings / (General) / Enable 32-Bit Applications**: False
2. Create a new website - Use default web.config in the Universal install dir 
    - Create a new folder, and copy in web.config from ``C:\Program Files (x86)\Universal`
    - **Add Website / Pyshical Path**: Path to your new folder with web.config
    - Select the New App Pool Created for Universal.
    - Enable Windows Authentication and disable Anonymous Authentication.


## Example "Working" Web Config

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
    </handlers>
      <aspNetCore processPath="dotnet" arguments="&quot;%ProgramFiles(x86)%\Universal\Universal.Server.dll&quot;" stdoutLogEnabled="true" stdoutLogFile=".\logs\log" forwardWindowsAuthToken="true"  />
  </system.webServer>
</configuration>
```