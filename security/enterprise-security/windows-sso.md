---
description: Windows Single-Sign On support for PowerShell Universal.
---

# Windows SSO

Windows Authentication, also know as Negotiate authentication, uses Kerberos or NTLM to authenticate without prompting the user for a password. It is primarily supported on Windows domains but can be configured in Linux and Mac OS.&#x20;

### appsettings.json

Windows Authentication provides single-sign on support for browsers and environments that support it. To enable Windows Authentication, set the `WindowsAuthentication` enabled setting to true in `appsettings.json`.

```javascript
"Windows": {
  "Enabled": "true"
},
```

### Authentication.ps1

You can enable Windows authentication by adding a new authentication provider in Security \ Authentication. Select Windows and enable the authentication.

![](<../../.gitbook/assets/image (340).png>)

Once Windows set to authenticated, Windows authentication can now be used against Universal. You will have to log out in order to use Windows authentication.

### Windows Authentication in IIS

To enable Windows Authentication in IIS, ensure that you enable Windows Authentication and disable anonymous authentication.

![](<../../.gitbook/assets/image (84).png>)

In the web.config file that is included with PowerShell Universal, ensure that you have set the `forwardWindowsAuthToken` to `true`.

```
<aspNetCore processPath="Universal.Server.exe" arguments="" forwardWindowsAuthToken="true" stdoutLogEnabled="true" stdoutLogFile=".\logs\log" hostingModel="OutOfProcess"/>
```

### Windows Authentication outside of IIS

Windows Authentication is supported outside of IIS but requires configuration of the account running the Universal service.

#### Windows

On Windows, you should install PowerShell Universal as a [Windows Service](../../getting-started/#windows). Once the service is installed, you will need to create a [service account user](../../config/running-as-a-service-account.md#application-service-account) and set the service to run with that user's account. The Windows authentication [setting ](../../config/settings.md)needs to be set to true.

```javascript
"Windows": {
  "Enabled": "true"
},
```

The service account needs to have a Service Principal Name (spn) configured for the computer account. You can do this using the `setspn` command. The computer name needs to be the full qualified name of the machine running Universal.

```
setspn -S HTTP/myservername.mydomain.com myuser
```

For more information, you can follow the Microsoft documentation for configuring ASP.NET Core Windows Authentication: [Configuring a Windows machine for Windows Authentication](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/windowsauth?view=aspnetcore-3.1\&tabs=visual-studio#windows-environment-configuration)

#### Linux

[Configuring a Linux or Mac OS machine for Windows Authentication](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/windowsauth?view=aspnetcore-3.1\&tabs=visual-studio#linux-and-macos-environment-configuration)

### Cached Claims

PowerShell Universal will cache group membership claims when using Windows Authentication. Claims are cached for the configured session timeout value (default is 25 minutes).

To clear the cache manually, navigate to Security \ Roles and click the Clear Cached Claims button.

## Browser Configuration

Depending on your local environment, you may need to configure your browser to properly pass credentials to PowerShell Universal.

* [Google Chrome](https://chromeenterprise.google/policies/#HTTPAuthentication)
* [Microsoft Edge](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies#http-authentication-policies)
