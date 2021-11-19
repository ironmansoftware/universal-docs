# Security

## Forms Authentication

{% hint style="warning" %}
The forms authentication script is only called when users login through the login page. If you use any other authentication method, this script is not called. Role policy scripts are called for all authentication types.
{% endhint %}

By default, the forms authentication script is configured to accept the user Admin and any password. You can configure this authentication policy to interact with whatever system you like. The script will receive a `PSCredential` object that contains the user name and password entered by the user at the login page.

{% hint style="info" %}
Authentication settings are also stored with `authentication.ps1`
{% endhint %}

To update forms authentication, you can click Settings  Security and then click the Settings button for the forms authentication.

![](<../../.gitbook/assets/image (300).png>)

You can update the PowerShell script found in settings to configure how the user is authenticated. You'll need to return a `New-PSUAuthenticationResult` from the script to indicate whether the user was successfully authenticated.

```powershell
param(
    [PSCredential]$Credential
)

#
#   You can call whatever cmdlets you like to conduct authentication here.
#   Just make sure to return the $Result with the Success property set to $true
#

if ($Credential.UserName -eq 'Admin') 
{
    New-PSUAuthenticationResult -Success -UserName 'Admin'
}
else 
{
    New-PSUAuthenticationResult -ErrorMessage 'Bad username or password'
}
```

### Setting a Password

You can check the password of the credential by using the `GetNetworkCredential()` method of `PSCredential`.

```powershell
param(
    [PSCredential]$Credential
)

#
#   You can call whatever cmdlets you like to conduct authentication here.
#   Just make sure to return the $Result with the Success property set to $true
#

if ($Credential.UserName -eq 'Admin' -and $Credential.GetNetworkCredential().Password -eq 'MySuperSecretPassword') 
{
    New-PSUAuthenticationResult -Success -UserName 'Admin'
}
else 
{
    New-PSUAuthenticationResult -ErrorMessage 'Bad username or password'
}
```

### Setting Claims

During forms authentication, you can set claims that will be available within role policies. This can provide a performance benefit when interacting with remote systems since you can perform a single claim lookup and then evaluate the claims locally rather than having to make additional calls to the remote system.

This example uses Active Directory to look up group membership and assign the as claims that will be available within the roles scripts.

```powershell
param(
    [PSCredential]$Credential
)

#
#   You can call whatever cmdlets you like to conduct authentication here.
#   Just make sure to return the $Result with the Success property set to $true
#

$Result = [Security.AuthenticationResult]::new()
if ($Credential.UserName -eq 'Admin') 
{
    #Maintain the out of box admin user
    New-PSUAuthenticationResult -UserName 'Admin' -Success
}
else
{
    # Get current domain using logged-on user's credentials - this validates their credential
    $CurrentDomain = "LDAP://DC=mydemodomain,DC=com"  # Insert Your Domain Here
    $domain = New-Object System.DirectoryServices.DirectoryEntry($CurrentDomain,($Credential.UserName),$Credential.GetNetworkCredential().password)

    if ($domain.name -eq $null)
    {
        "Authentication failed for $($Credential.UserName)!" | Out-File "C:\test\adlogin.txt"
        write-host "Authentication failed - please verify your username and password."
        New-PSUAuthenticationResult -UserName $Credential.UserName
    }
    else
    {
        write-host "Successfully authenticated with domain $($domain.name)"
        "Authentication success for $($Credential.UserName)!" | Out-File "C:\test\adlogin.txt"

        New-PSUAuthenticationResult -UserName $Credential.UserName -Success -Claims { 
            Get-ADPrincipalGroupMembership $Credential.UserName | Select-Object -ExpandProperty name | ForEach-Object {
                New-PSUAuthorizationClaim -Type Role -Value $_
            }
        }
    }
}
```

Within your `roles.ps1` file, you will be able to use these claims to validate group membership.

This example checks to see if the user is part of the SOC\_Admins group.

```powershell
param($User)

$Roles = $User.Claims | Where-Object Type -eq Role | Select-Object -ExpandProperty Value
$Roles -contains 'SOC_Admins'
```

### Variables&#x20;

These are the variables defined within the security scripts.

| Name             | Description                                    | Type      |
| ---------------- | ---------------------------------------------- | --------- |
| $Cookies         | Cookies provided in the client's HTTP request. | hashtable |
| $Headers         | Headers provided in the client's HTTP request. | hashtable |
| $LocalIpAddress  | The local IP address of the request.           | string    |
| $LocalPort       | The local port of the request.                 | string    |
| $RemoteIpAddress | The remote IP address of the request.          | string    |
| $RemotePort      | The remote port of the request.                | string    |

## OpenID Authentication

You can configure OpenID authentication and authorization by adjusting the settings within the `OpenID` section of the `appsettings.json` file. Authorization policies that you configure within Universal will be run on the user's identity after authentication is successful.

## Windows Authentication

### appsettings.json

Windows Authentication provides single-sign on support for browsers and environments that support it. To enable Windows Authentication, set the `WindowsAuthentication` enabled setting to true in `appsettings.json`.

```javascript
"Windows": {
  "Enabled": "true"
},
```

### Authentication.ps1

{% hint style="info" %}
Available in PowerShell Universal 2.5 and later.&#x20;
{% endhint %}

You can enable Windows authentication by adding a new authentication provider in Security \ Authentication. Select Windows and enable the authentication.&#x20;

![](<../../.gitbook/assets/image (294).png>)

Once Windows set to authenticated, Windows authentication can now be used against Universal. You will have to log out in order to use Windows authentication.

### Windows Authentication in IIS

To enable Windows Authentication in IIS, ensure that you enable Windows Authentication and disable anonymous authentication.

![](<../../.gitbook/assets/image (149).png>)

In the web.config file that is included with PowerShell Universal, ensure that you have set the `forwardWindowsAuthToken` to `true`.

```
<aspNetCore processPath="Universal.Server.exe" arguments="" forwardWindowsAuthToken="true" stdoutLogEnabled="true" stdoutLogFile=".\logs\log" hostingModel="OutOfProcess"/>
```

### Windows Authentication outside of IIS

Windows Authentication is supported outside of IIS but requires configuration of the account running the Universal service.

#### Windows

On Windows, you should install PowerShell Universal as a [Windows Service](../../getting-started/#windows). Once the service is installed, you will need to create a [service account user](../running-as-a-service-account.md#application-service-account) and set the service to run with that user's account. The Windows authentication [setting ](../settings.md)needs to be set to true.

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

## Authorization

{% embed url="https://youtu.be/0lqyb-PdCxc" %}

User authorization is accomplished with roles. Roles are either assigned based on the policy script you define or a role is assigned manually to the user.

### Policy Assignment

By default, roles are assigned by policies. Policies are run when the user logs in. You can change the policy scripts by visiting the Security / Roles tab. Click the Edit Policy button to configure the Policy script.

![](<../../.gitbook/assets/image (8).png>)

Policy scripts will receive a `ClaimsPrincipal` object as a parameter and need to return true or false. Policies that throw errors will be assumed to be false. The `ClaimsPrincipal` object contains the user's identity and the claims that the user has received. These may include group assignments or other features of a user's account.

You can expect an object with this structure.

```csharp
public class ClaimsPrincipal
{
    public List<Claim> Claims { get; set; } = new List<Claim>();
    public Identity Identity { get; set; } = new Identity();
}

public class Identity 
{
    public string Name { get ;set; }
}

public class Claim 
{
    public string Type { get; set; }  
    public string Value { get; set; }
    public string ValueType { get; set; } 
    public string Issuer { get; set; }
    public Dictionary<string, string> Properties { get; set; } = new Dictionary<string, string>();
}
```

### Role Assignment

To assign a role to a user, you can create their identity within Universal and then select the role in the drop down on the Identities page. By default, identities receive a role through policy.

![](<../../.gitbook/assets/image (18).png>)

### Built in Roles

#### Administrator

Full access to the entire PowerShell Universal platform and settings.

#### Operator

Operators have access to add and remove resources such as APIs, Scripts and Dashboards. Operators cannot change settings like environments, roles, or general settings.

#### Execute

The Execute role grants the ability to run scripts and read access for everything else.

#### Reader

The Reader role provides read-only access to PowerShell Universal.

### Users with Many Groups

If your users are members of more than about 40 groups you may experience problems logging in. This is due to size limits of the HTTP headers in IIS and Kestrel. The more groups a user is a member of, the more authorization claims they have and the large the header.

You can increase the header limit for Kestrel by using the limits configuration in `appsettings.json` file. You will need to increase the header size. It is a value in bytes and defaults to 32kb.

```
{
  "Kestrel": {
    "Endpoints": {
      "HTTP": {
        "Url": "http://*:5000"
      }
    },
    "Limits": {
      "MaxRequestHeadersTotalSize": 132768
    },
    "RedirectToHttps": "false"
  },
```

### IIS Authorization

Authorization in IIS works as with any other method but you need to be aware of the request header size limit. You may receive errors when you enable claims that include many groups. They can exceed the header size limit and IIS will return errors. We have found that about 40 Azure Active Directory groups will cause this issue on a default IIS installation.

The error you will receive will either be a 400 error with the request is too long.

![](<../../.gitbook/assets/image (150).png>)

If you have HTTPS enabled, you will receive an error about a HTTP2 protocol error.

![](<../../.gitbook/assets/image (4).png>)

You can increase the IIS request size by setting the following registry keys. You will need to restart you machine in order for them to take affect.

```
HKLM:\System\CurrentControlSet\Services\Http\Parameters
    MaxFieldLength: DWORD

HKLM:\System\CurrentControlSet\Services\Http\Parameters
    MaxRequestBytes: DWORD
```

More information can be found on [Microsoft's documentation](https://docs.microsoft.com/en-us/troubleshoot/iis/http-bad-request-response-kerberos#workaround-2-set-maxfieldlength-and-maxrequestbytes-registry-entries).

As an alternative to increasing the request size, you can also reduce the number of groups sent. In Azure Active Directory, you can set to just the groups assigned to the application to prevent all groups from being sent.

In Azure go to **App registrations** > (Select the app) > **Token Configuration**, and specify Groups assigned to the application. ![](https://support.ironmansoftware.com/api/v1/threads/548223000001702109/inlineImages/edbsndabe757f382adbd6bf97fb8f980f999a0299e9db01c2972b353b3c8c4ffe29e6ae82d11d75341af2d224cd8f4103b9b009cb9d18e2809c18ece1c19c88900fe13e6b2866bb6604db1b7c9360f4da552d?et=17798841e64\&ha=5d1aea069a1f58d946c8dad4e93abec12ca48d705aad7500a321b0c311d7e581\&f=1.png)

Now go to **Enterprise Application** > (Select the app) > **Users and groups**. Assign the group(s) you are interested in including in the claims. (Note: this can also be used as a security boundary if you set “User Assignment Required” to Yes in the ‘Properties’ section of the app)

![](https://support.ironmansoftware.com/api/v1/threads/548223000001702109/inlineImages/edbsndabe757f382adbd6bf97fb8f980f999a0299e9db01c2972b353b3c8c4ffe29e6ae82d11d75341af2d224cd8f4103b9b0ba101ed249f6cf46a1cf05c5cfe5650d84cedc32ef9ab20a4535665ec422da7b?et=17798841e64\&ha=0397e6316da5e7ab913c1ec8c932ba854c1a88d27c54044ea299ca2dac438aef\&f=2.png)

## App Tokens

App Tokens can be assigned to services that cannot login interactively. You can grant a new app token to your account by clicking the Grant App Token button within the Security / App Tokens tab.

The token will have a expiration of one year and have the valid roles for your account. To copy the App Token to your account, click the Copy action. To revoke an App Token, click the Revoke action.

You can use App Tokens with the Universal cmdlets or by using web requests directly using Bearer authorization.

![](<../../.gitbook/assets/image (5).png>)

## Environment

By default, the forms authentication and policy assignment scripts run within the PowerShell Universal process. You can optional configure an external [Environment ](../environments.md)to run your authentication and authorization scripts. When you configure a security environment, an external PowerShell process will be started and configured use your Environment's settings.

To adjust the environment used by the security process, set the `-SecurityEnvironment` in `settings.ps1`.

```powershell
Set-PSUSetting -SecurityEnvironment '5.1'
```

## Example: Forms Authentication with Active Directory

The following example shows performing a simple "LDAP BIND" in order to validate a users Active Directory Credentials. If a user attempting to access PowerShell Universal is not the Default Admin User they will have to successfully authenticate their credentials with Active Directory via a simple LDAP bind. This can be combined with a AD Group Member check in the Admin, Operator, and Reader role policies to effectively use Active Directory Authentication AND Active Directory Group membership to provide Role Based Access to PowerShell Universal.

```powershell
param(
    [PSCredential]$Credential
)

#
#   You can call whatever cmdlets you like to conduct authentication here.
#   Just make sure to return the $Result with the Success property set to $true
#

$Result = [Security.AuthenticationResult]::new()
if ($Credential.UserName -eq 'Admin') 
{
    #Maintain the out of box admin user
    $Result.UserName = 'Default Admin'
    $Result.Success = $true 
}
else
{
    # Get current domain using logged-on user's credentials - this validates their credential
    $CurrentDomain = "LDAP://DC=mydemodomain,DC=com"  # Insert Your Domain Here
    $domain = New-Object System.DirectoryServices.DirectoryEntry($CurrentDomain,($Credential.UserName),$Credential.GetNetworkCredential().password)

    if ($domain.name -eq $null)
    {
        "Authentication failed for $($Credential.UserName)!" | Out-File "C:\test\adlogin.txt"
        write-host "Authentication failed - please verify your username and password."
        $Result.UserName = ($Credential.UserName)
        $Result.Success = $false 
    }
    else
    {
        write-host "Successfully authenticated with domain $($domain.name)"
        "Authentication success for $($Credential.UserName)!" | Out-File "C:\test\adlogin.txt"
        $Result.UserName = ($Credential.UserName)
        $Result.Success = $true 
    }
}

$Result
```

## Example: Policy based on Active Directory Group Membership (Windows Authentication)

{% hint style="info" %}
This example requires an authentication method that will provide group information during the authentication process. Methods like Windows authentication and WS-Federation can provide this information. Forms authentication will not work with this type of policy.
{% endhint %}

This example takes advantage of the claims that are provided during authentication. You can check to see if the user has a groupsid (group membership) by using the `HasClaim` method of the `$User` object. This method will check the `Claims` array to see if they have a particular `groupsid` claim. Use the SID of the group to validate whether they are a group member.

```powershell
New-PSURole -Name 'Administrators' -Policy {
    param(
        $User
    )

    $User.HasClaim("http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 'S-1-5-21-22222222-111111-3333333-153')
}
```

For debugging and development purposes, you can check to see what claims a user has been exporting the `$User` variable to a file.

```powershell
New-PSURole -Name 'Administrators' -Policy {
    param(
        $User
    )

    $User | ConvertTo-Json | Out-File .\myUser.json

    $User.HasClaim("http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 'S-1-5-21-22222222-111111-3333333-153')
}
```

You should see a JSON file that contains the user's identity and claims array.

```javascript
{
  "Claims": [
    {
      "Type": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
      "Value": "LAPTOP-496LAUK8\\adamr",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid",
      "Value": "S-1-5-21-1001",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-1-0",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid",
      "Value": "S-1-5-114",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-5-21-1002",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid",
      "Value": "S-1-5-32-544",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-5-32-559",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-5-32-545",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-5-4",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-2-1",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-5-11",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-5-15",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-11-96-977963020-1793067495-765970767",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-5-113",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-2-0",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
      "Value": "S-1-5-64-36",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "AD AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    }
  ],
  "Identity": {
    "Name": "LAPTOP-496LAUK8\\adamr"
  }
}
```

## Example: Policy based on Active Directory Group Membership

In this example we will configure out Administrator Policy Script to use LDAP to retrieve the membership of an Active Directory Group. Here we have created a group called "PowerShell Universal Admins" where members of the group should be granted Administrator Access in PowerShell Universal. Here we are doing a simple samaccountname check for the user to ensure they are a member of the group. For more robust environments a SID/DN/ObjectGUID check would be more appropriate.

![](<../../.gitbook/assets/image (15).png>)

```powershell
param(
$User
)

$UserName = ($User.Identity.Name)
$UserName = $UserName.Substring($UserName.IndexOf('\')+1,($UserName.Length -($UserName.IndexOf('\')+1)))

$IsMember = $false;

# Perform LDAP Group Member Lookup
$Searcher = New-Object DirectoryServices.DirectorySearcher
$Searcher.SearchRoot = 'LDAP://CN=Users,DC=berg,DC=com' # INSERT ROOT LDAP HERE
$Searcher.Filter = "(&(objectCategory=person)(memberOf=CN=PowerShell Universal Admins,OU=Information Technology,DC=berg,DC=com))" #GROUP INSERT DN TO CHECK HERE
$Users = $Searcher.FindAll()
$Users | ForEach-Object{
    If($_.Properties.samaccountname -eq $UserName)
    {
        $IsMember = $true;
        "$UserName is a member of admin group!" | Out-File "C:\test\adgroup.txt"
    }
    else {
        "$UserName is NOT member of admin group!" | Out-File "C:\test\adgroup.txt"
    }
}

return $IsMember
```

## Example: Group membership based on Azure Active Directory

This example takes advantage of [OpenID Connect and Azure Active Directory](openid-connect.md#configuring-azuread).&#x20;

Once you have configured PowerShell Universal and Azure Active Directory, you can configure role scripts to verify whether users are members of groups found in Azure AD. You can take advantage of the `HasClaim` method of the `$User` variable to check membership.

First, ensure that you have group membership claims enabled in the manifest for your application registration. This will include all group membership so it is accessible in PowerShell Universal.&#x20;

![](<../../.gitbook/assets/image (231).png>)

```
"groupMembershipClaims": "All",
```

Once configured, you can update your role script to check for a group membership. First make note of the object ID of the group you are looking to check within Azure AD.&#x20;

![](<../../.gitbook/assets/image (232).png>)

Next, within your `roles.ps1` script, you can validate a user has a particular role by using `HasClaim` and providing the object GUID.&#x20;

```powershell
param(
$User
)
        
$User.HasClaim("groups", "4acabc67-56cc-4590-9de6-164f3c4faf10") 
```

As users login, their group membership will be validated against their claims and a role will be assigned.
