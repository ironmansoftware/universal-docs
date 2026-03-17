---
description: All about the Universal PowerShell module.
---

# Module

## Connecting to PowerShell Universal

The PowerShell Universal module requires a few bits of information to connect to the server. First, it needs to know the URL or computer name, second it needs credentials in order to access the resources remotely.

You can use the `Connect-PSUServer` cmdlet to setup a connection to the server. Calling this cmdlet sets the connection information for the entire process. If you are running in a multi-user process, you need to consider the implications of using this command.

```powershell
Connect-PSUServer -ComputerName http://localhost:5000 -AppToken xyz123
```

When running scripts in the Integrated environment or within Apps or APIs in PowerShell Universal, consider using the Computer Name and credentials values for the cmdlets directly to avoid sharing them across the process.

```powershell
Get-PSUJob -ComputerName http://localhost:5000 -AppToken xyz123
```

### Authentication

### App Token

You can use the `-AppToken` parameter to authentication against the API with the specified token. Treat the App Token as a password as it grants access based on the roles assigned to it.

### Default Credentials

You can use Default Credentials, or Windows Credentials, as well. This mechanism is only support if the target server has Windows Authentication enabled. Roles and permissions will be granted when connecting to the server.

### Credentials

If you have form authentication enabled, you can use Basic authentication by specifying a `PSCredential` object to the `-Credential` parameter of `Connect-PSUServer`.

### Scope

`Connect-PSUServer` supports a scope parameter to define how to persist the connection information. By default, the scope is Process. The process scope stores the connection information in a static .NET scope. All cmdlets run in the current process will use this connection information.

If you are using `Connect-PSUServer` in a multi-runspace environment, like the Integrated environment or within apps in PowerShell Universal, you may want to only store the connection information for the current runspace. Use the `-Scope Runspace` parmaeter value to adjust how the connection information is stored.

### Disconnecting

You can disconnect from the PowerShell Universal server by using the `Disconnect-PSUServer` cmdlet. If you have used the Runspace scope, it will clear the necessary variables and if you used the Process scope, it will clear the necessary static properties.

## Internal Connections

When using the Universal module within PowerShell Universal, it isn't necessary to specify credentials of the computer name in basic installations. Authorization will match the current user, and the API URL will be inferred from the current server.

### Authorization

When using the Strict security model, authorization is based on the caller. For example, if a user calls and API endpoint and that endpoint calls `Invoke-PSUScript`, the call is on behalf of the endpoint caller. Permissions of the caller are enforced on the script execution.&#x20;

When using other security models, the cmdlets are called on behalf of the System user and authorization is not enforced based on the caller of the resource.&#x20;

#### Authorization Security Model

You can change the authorization model to allow any calls from within PowerShell Universal to function without an app token. While this may be considered less secure by some, it depends on your organization's use of the platform. This value can be set in `appsettings.json` or within the `API__SecurityModel` environment variable.

A user context is required for authentication. This means that when using the module in non-user contexts, like the Schedules, you will need to provide an app token.

In scopes that have a user context, like an app, calls to cmdlets are made under that user's privileges. For example, if a user accessing an app doesn't have access to call `Get-PSUScript`, the cmdlet will not be usable without an app token with those privileges.

```json
{
    "Api": {
       "SecurityModel": "Strict"
    }
}
```

Permissive mode still uses the external PowerShell Universal APIs and communicates the user context, if available, when calling the PowerShell Universal APIs. Permissive mode allows the use of the -Integrated switch to bypass authorization and to use the back-channel TCP connection rather than the PowerShell Universal external API.

```json
{
    "Api": {
       "SecurityModel": "Permissive"
    }
}
```

You can also use the `Integrated` Security Model to completely avoid the need to configure app tokens, URLs or certificates. The Integrated Security Model does not communicate the user context, even when the user is authenticated. It also uses the back-channel TCP connection rather than the PowerShell Universal external API.

```json
{
    "Api": {
       "SecurityModel": "Integrated"
    }
}
```

#### Trust HTTPS Certificate

In some environments, it may be required to allow PowerShell Universal to trust the certificate of the web server in order for it to communicate successfully. On each call, you can use the `-TrustCertificate` parameter to allow to behavior. Additionally, you can set the value at a server level to allow for internal communications.

```json
{
    "Api": {
       "TrustCertificate": true
    }
}
```

### Integrated Mode

Integrated mode uses the internal PowerShell Universal backchannel connection to communicate with the services via the Universal module. When using Integrated mode, authorization is only performed when the API is in Strict security mode.&#x20;

You can invoke cmdlets using integrated mode by using the `-Integrated` switch parameter.&#x20;

The server Security Model can also be set to `Integrated`. This forces all cmdlet calls to use the integrated mode and no longer requires the use of the `-Integrated` parameter.

### Schedules

Schedules do not have a current user. You will need to specify an App Token or Default Credential when using cmdlets within scheduled scripts. Although this is an extra step, it ensures that only the necessary permissions are applied to the schedule script.

Schedules do not have a user context so you will need to specify one in order to get them to run properly when using these cmdlets.

### Reverse Proxies (IIS)

PowerShell Universal uses all available data to determine the proper URL to call when using the API. This can be problematic when using a reverse proxy, like IIS. The URL that PowerShell Universal sees is different than the actual, accessible URL. This can cause problems when the cmdlets attempt to access the API.

To work around this problem, you can either specify the proper URL for each cmdlet call or you can customize the API URL in the application settings.

#### Specify the URL

To specify the URL, just provide it to the `-ComputerName` parameter.

```powershell
Get-PSUJob -ComputerName 'https://external.company.com/psu'
```

#### Application Settings

You can also set the application settings API URL value to provide the same value across the platform. Either set the value in an environment variable or within the `appsettings.json` file.

```json
{
  "API": {
    "URL": "https://external.company.com/psu"
  }
}
```

## Technical Considerations

The Universal module uses gRPC for all communication with the PowerShell Universal server. Depending on the server configuration, the gRPC communication will be slightly different.

### HTTPS

When using HTTPS, the standard gRPC communication channel will be used. This is the fastest configuration because it does not require special serialization or accommodations for down-level protocols. HTTP/2 is required for gRPC.

If HTTPS is used, the certificate must be trusted by the system. If the certificate is self-signed, you can use the `-TrustCertificate` parameter on the cmdlets to avoid the certificate check.

### HTTP and Windows Authentication

When using HTTP or Windows Authentication, HTTP/2 is not supported and gRPC cannot run natively because trailing headers are not supported. To accommodate this, the Universal module will use a technology call gRPC-Web to translate gRPC calls to HTTP and JSON in order call HTTP REST methods rather than the standard gRPC methods.

This configuration is slightly slower but shouldn't be noticeable in most environments.

### Integrated Mode

Integrated mode does not use the external API and communicates across the gRPC backchannel of PowerShell Universal. There is no need to configure API URLs, certificates or credentials.
