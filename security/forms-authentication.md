---
description: Forms authentication scripts in PowerShell Universal.
---

# Forms Authentication

{% hint style="warning" %}
The forms authentication script is only called when users login through the login page. If you use any other authentication method, this script is not called. Role policy scripts are called for all authentication types.
{% endhint %}

By default, the forms authentication script is configured to accept the user Admin and any password. You can configure this authentication policy to interact with whatever system you like. The script will receive a `PSCredential` object that contains the user name and password entered by the user at the login page.

{% hint style="info" %}
Authentication settings are also stored with `authentication.ps1`
{% endhint %}

To update forms authentication, you can click Settings Security and then click the Settings button for the forms authentication.

![](<../.gitbook/assets/image (251).png>)

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

## Setting a Password

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

## Setting Claims

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

## Variables

These are the variables defined within the security scripts.

| Name             | Description                                    | Type      |
| ---------------- | ---------------------------------------------- | --------- |
| $Cookies         | Cookies provided in the client's HTTP request. | hashtable |
| $Headers         | Headers provided in the client's HTTP request. | hashtable |
| $LocalIpAddress  | The local IP address of the request.           | string    |
| $LocalPort       | The local port of the request.                 | string    |
| $RemoteIpAddress | The remote IP address of the request.          | string    |
| $RemotePort      | The remote port of the request.                | string    |

## Basic Authentication

When calling API endpoints or the PowerShell Management API, you can use Basic authentication to pass in a user name and password. This will invoke the forms authentication and authorization scripts to valid the login. The username and password should be encoded as Base64 in the `username:password` format and sent in the Authorization header with a `Basic` prefix.

```powershell
$credentials = [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes("admin:admin"))
Invoke-RestMethod $Env:UniversalUrl/api/v1/accessible -Headers @{
    Authorization = "Basic $credentials"
} 
```

You can also use the built-in -Credential parameter on Invoke-RestMethod to avoid having to encode the basic credentials yourself. The `$AdminCredential` below needs to be a `PSCredential`.

```powershell
Invoke-RestMethod $Env:UniversalUrl/api/v1/accessible -Credential $AdminCredential -Authentication Basic
```

## Live Log

You can use the live log view on the authentication page to view information about the script execution. The live log view will display PowerShell streams.
