---
description: All about the Universal PowerShell module.
---

# Module

## Connecting to PowerShell Universal

The PowerShell Universal module requires a few bits of information to connect to the server. First, it needs to know the URL or computer name, second it needs credentials in order to access the resources remotely.&#x20;

You can use the `Connect-PSUServer` cmdlet to setup a connection to the server. Calling this cmdlet sets the connection information for the entire process. If you are running in a multi-user process, you need to consider the implications of using this command.&#x20;

```powershell
Connect-PSUServer -ComputerName http://localhost:5000 -AppToken xyz123
```

When running scripts in the Integrated environment or within Apps or APIs in PowerShell Universal, consider using the Computer Name and credentials values for the cmdlets directly to avoid sharing them across the process.

```powershell
Get-PSUJob -ComputerName http://localhost:5000 -AppToken xyz123
```

### Authentication

### App Token

You can use the `-AppToken` parameter to authentication against the API with the specified token.  Treat the App Token as a password as it grants access based on the roles assigned to it.&#x20;

### Default Credentials&#x20;

You can use Default Credentials, or Windows Credentials, as well. This mechanism is only support if the target server has Windows Authentication enabled. Roles and permissions will be granted when connecting to the server.&#x20;

## Internal Connections

When using the Universal module within PowerShell Universal, it isn't necessary to specify credentials of the computer name in basic installations. Authorization will match the current user, and the API URL will be inferred from the current server.&#x20;

### Authorization

Calls to the Universal cmdlets do not require additional authorization when run within the Universal server. That said, they will run in the context of the user that is calling the Script, API or App. For example, if an API Reader calls an API that then calls the `Get-PSUJob` cmdlet, they will not have access because their context does not allow it.&#x20;

The API developer can work around this by providing an App Token that does have the necessary permissions.&#x20;

#### Authorization Security Model&#x20;

You can change the authorization model to allow any calls from within PowerShell Universal to function without an app token. While this may be considered less secure by some, it depends on your organization's use of the platform. This value can be set in `appsettings.json` or within the `API__SecurityModel` environment variable.

```json
{
    "Api": {
       "SecurityModel": "Permissive"
    }
}
```

#### Trust HTTPS Certificate

In some environments, it may be required to allow PowerShell Universal to trust the certificate of the web server in order for it to communicate successfully. On each call, you can use the `-TrustCertificate` parameter to allow to behavior. Additionally, you can set the value at a server level to allow for internal communications.&#x20;

```json
{
    "Api": {
       "TrustCertificate": true
    }
}
```

### Schedules

Schedules do not have a current user. You will need to specify an App Token or Default Credential when using cmdlets within scheduled scripts. Although this is an extra step, it ensures that only the necessary permissions are applied to the schedule script.&#x20;

Schedules do not have a user context so you will need to specify one in order to get them to run properly when using these cmdlets.&#x20;

### Reverse Proxies (IIS)

PowerShell Universal uses all available data to determine the proper URL to call when using the API. This can be problematic when using a reverse proxy, like IIS. The URL that PowerShell Universal sees is different than the actual, accessible URL. This can cause problems when the cmdlets attempt to access the API.&#x20;

To work around this problem, you can either specify the proper URL for each cmdlet call or you can customize the API URL in the application settings.&#x20;

#### Specify the URL

To specify the URL, just provide it to the `-ComputerName` parameter.&#x20;

```powershell
Get-PSUJob -ComputerName 'https://external.company.com/psu'
```

#### Application Settings

You can also set the application settings API URL value to provide the same value across the platform. Either set the value in an environment variable or within the `appsettings.json` file.&#x20;

```json
{
  "API": {
    "URL": "https://external.company.com/psu"
  }
}
```

## Technical Considerations

The Universal module uses gRPC for all communication with the PowerShell Universal server. Depending on the server configuration, the gRPC communication will be slightly different.&#x20;

### HTTPS

When using HTTPS, the standard gRPC communication channel will be used. This is the fastest configuration because it does not require special serialization or accommodations for down-level protocols. HTTP/2 is required for gRPC.&#x20;

If HTTPS is used, the certificate must be trusted by the system. If the certificate is self-signed, you can use the `-TrustCertificate` parameter on the cmdlets to avoid the certificate check.&#x20;

### HTTP and Windows Authentication

When using HTTP or Windows Authentication, HTTP/2 is not supported and gRPC cannot run natively because trailing headers are not supported. To accommodate this, the Universal module will use a technology call gRPC-Web to translate gRPC calls to HTTP and JSON in order call HTTP REST methods rather than the standard gRPC methods. &#x20;

This configuration is slightly slower but shouldn't be noticeable in most environments.&#x20;
