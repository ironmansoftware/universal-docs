# Security

## Forms Authentication

By default, the forms authentication script is configured to accept the user Admin and any password. You can configure this authentication policy to interact with whatever system you like. The script will receive a `PSCredential` object that contains the user name and password entered by the user at the login page. 

{% hint style="info" %}
Authentication settings are also stored with `authentication.ps1`
{% endhint %}

To update forms authentication, you can click Settings \ Security and then click the Settings button for the forms authentication. 

![](../../.gitbook/assets/image%20%28179%29.png)

You can update the PowerShell script found in settings to configure how the user is authenticated. You'll need to return a `New-PSUAuthenticationResult` from the script to indicate whether the user was successfully authenticated. 

```text
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

## OpenID Authentication

You can configure OpenID authentication and authorization by adjusting the settings within the `OpenID` section of the `appsettings.json` file. Authorization policies that you configure within Universal will be run on the user's identity after authentication is successful.

## Windows Authentication

Windows Authentication provides single-sign on support for browsers and environments that support it. To enable Windows Authentication, set the `WindowsAuthentication` enabled setting to true in `appsettings.json`. 

```text
"Windows": {
  "Enabled": "true"
},
```

### Windows Authentication in IIS 

To enable Windows Authentication in IIS, ensure that you enable Windows Authentication and disable anonymous authentication.

![](../../.gitbook/assets/image%20%28149%29.png)

### Windows Authentication outside of IIS

Windows Authentication is supported outside of IIS but requires configuration of the account running the Universal service. 

#### Windows

On Windows, you should install PowerShell Universal as a [Windows Service](../../get-started/getting-started/#windows). Once the service is installed, you will need to create a [service account user](../running-as-a-service-account.md#application-service-account) and set the service to run with that user's account. The Windows authentication [setting ](../settings.md)needs to be set to true. 

```text
"Windows": {
  "Enabled": "true"
},
```

The service account needs to have a Service Principal Name \(spn\) configured for the computer account. You can do this using the `setspn` command. The computer name needs to be the full qualified name of the machine running Universal. 

```text
setspn -S HTTP/myservername.mydomain.com myuser
```

For more information, you can follow the Microsoft documentation for configuring ASP.NET Core Windows Authentication: [Configuring a Windows machine for Windows Authentication](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/windowsauth?view=aspnetcore-3.1&tabs=visual-studio#windows-environment-configuration)

#### Linux

[Configuring a Linux or Mac OS machine for Windows Authentication](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/windowsauth?view=aspnetcore-3.1&tabs=visual-studio#linux-and-macos-environment-configuration)

## Authorization 

{% embed url="https://youtu.be/0lqyb-PdCxc" %}

User authorization is accomplished with roles. Roles are either assigned based on the policy script you define or a role is assigned manually to the user.  

### Policy Assignment

By default, roles are assigned by policies. Policies are run when the user logs in. You can change the policy scripts by visiting the Security / Roles tab. Click the Edit Policy button to configure the Policy script. 

![](../../.gitbook/assets/image%20%288%29.png)

Policy scripts will receive a `ClaimsPrincipal` object as a parameter and need to return true or false. Policies that throw errors will be assumed to be false. The `ClaimsPrincipal` object contains the user's identity and the claims that the user has received. These may include group assignments or other features of a user's account. 

You can expect an object with this structure. 

```text
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

![](../../.gitbook/assets/image%20%2818%29.png)

### Built in Roles

#### Administrator

Full access to the entire PowerShell Universal platform and settings. 

#### Operator

Operators have access to add and remove resources such as APIs, Scripts and Dashboards. Operators cannot change settings like environments, roles, or general settings. 

#### Execute

The Execute role grants the ability to run scripts and read access for everything else. 

#### Reader

The Reader role provides read-only access to PowerShell Universal.

## App Tokens

App Tokens can be assigned to services that cannot login interactively. You can grant a new app token to your account by clicking the Grant App Token button within the Security / App Tokens tab. 

The token will have a expiration of one year and have the valid roles for your account. To copy the App Token to your account, click the Copy action. To revoke an App Token, click the Revoke action. 

You can use App Tokens with the Universal cmdlets or by using web requests directly using Bearer authorization. 

![](../../.gitbook/assets/image%20%285%29.png)

## Environment

By default, the forms authentication and policy assignment scripts run within the PowerShell Universal process. You can optional configure an external [Environment ](../environments.md)to run your authentication and authorization scripts. When you configure a security environment, an external PowerShell process will be started and configured use your Environment's settings. 

To adjust the environment used by the security process, set the `-SecurityEnvironment` in `settings.ps1`. 

```text
Set-PSUSetting -SecurityEnvironment '5.1'
```

## Example: Forms Authentication with Active Directory

The following example shows performing a simple "LDAP BIND" in order to validate a users Active Directory Credentials. If a user attempting to access PowerShell Universal is not the Default Admin User they will have to successfully authenticate their credentials with Active Directory via a simple LDAP bind. This can be combined with a AD Group Member check in the Admin, Operator, and Reader role policies to effectively use Active Directory Authentication AND Active Directory Group membership to provide Role Based Access to PowerShell Universal.

```text
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

## Example: Policy based on Active Directory Group Membership

In this example we will configure out Administrator Policy Script to use LDAP to retrieve the membership of an Active Directory Group. Here we have created a group called "PowerShell Universal Admins" where members of the group should be granted Administrator Access in PowerShell Universal. Here we are doing a simple samaccountname check for the user to ensure they are a member of the group. For more robust environments a SID/DN/ObjectGUID check would be more appropriate.

![](../../.gitbook/assets/image%20%2815%29.png)

```text
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

