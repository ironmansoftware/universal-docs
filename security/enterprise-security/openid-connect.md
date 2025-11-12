---
description: Configure OpenID Connect with Universal.
---

# OpenID Connect

{% hint style="info" %}
OpenID Connect requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

OpenID Connect is an authentication layer on top of OAuth 2.0, an authorization framework. It is supported by many vendors and provides the ability to authenticate against systems like EntraID.

This document will outline the steps necessary to configure EntraID OpenID Connect and use it with Universal.

## Configuring Azure Entra ID (Azure Active Directory)

Within the Azure Portal, navigate to your Entra ID blade. Next, click the Enterprise Application node and then click New application.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Next, click Create your own application.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Select a name for your application and select Register an application to integrate with Microsoft Entra ID.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

In the Register an application page, define a redirect URI. This will be the URL of PowerShell Universal server that Entra ID will redirect the user to. This value is defined in the PowerShell Universal configuration file, `appsettings.json`.

Now that the application has been created, from the Enterprise Applications page, click Single sign-on and then Go to application. This will bring you to the application registration page.

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Certificates and secrets and define a new secret. This will be used with the PowerShell Universal configuration file.

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Now, we'll need to capture several points of information from the application to provide to PowerShell Universal. From the application's home page, save the Application (client) and directory (tenant) ID.

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Claim Mapping

In order to provide group claims to PowerShell Universal, you will need to expose the group claims from your app registration. Click Token Configuration and then click Add groups claim.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Entra ID Group Claims</p></figcaption></figure>

After clicking Add groups claim, you will have the option to select which groups are provided. If you select All Groups, the groups claims will be provided to PowerShell Universal

If you select Groups assigned to the application, ensure that you check the Emit groups as role claims value. This setting requires a paid Entra ID plan.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Emit groups as role claims setting</p></figcaption></figure>

To assign a group to your app registration, locate your app in Enterprise Applications and click User and Groups. Next, click Add User\Group and select the groups you would like assigned to your application.

Once you have the groups claim configured in Entra ID, you can then update PowerShell Universal claim mappings to the groups provided.

For each role you would like to assign to an Entra ID group, specify the Claim Type and Claim Value for that role. For example, I have a group in my environment with the ID 446832da-d4ad-4972-b0a2-eda736129928. The Claim Type for this object is [http://schemas.microsoft.com/ws/2008/06/identity/claims/groups](http://schemas.microsoft.com/ws/2008/06/identity/claims/groups).

To assign this to the administrator group, I would do the following.

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption><p>Claim Mapping</p></figcaption></figure>

Users of this group would now be part of the Administrator role in PowerShell Universal.

### Group Overages

For organizations that have users with many groups, you will want to limit the number of groups sent to PowerShell Universal. Sending large numbers of groups can exceed the size of the token and cause authorization failures. If you wish to limit the groups, select Groups assigned to the application.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

To add groups to the application, navigate back to the Enterprise application's page and select Users and groups.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Click the Add user/group value to assign these groups to your application. When users login to PowerShell Universal, only these group claims will be provided.

To learn more about Group Overages, [click here](https://learn.microsoft.com/en-us/security/zero-trust/develop/configure-tokens-group-claims-app-roles#group-overages).

### Configuring Universal for Entra ID

#### Use Appsettings.json

{% hint style="info" %}
Read more about `appsettings.json` on our [Settings ](../../config/settings.md)page.
{% endhint %}

Now that we have completed the configuration of an AzureAD App Registration, we can update the `appsettings.json` file with the appropriate settings. For my application, it would look something like this.

```javascript
    "OIDC": {
      "Enabled": "true",
      "CallbackPath": "/auth/signin-oidc",
      "ClientID": "<application ID>",
      "ClientSecret": "<client secret>",
      "Resource": "",
      "Authority": "https://login.microsoftonline.com/<directory ID>",
      "ResponseType": "code",
      "SaveTokens": "false",
      "GetUserInfo": false
    },
```

{% hint style="warning" %}
If you are using Chrome, you will also need to enable HTTPS. You will see a 500 error without HTTPS enabled.
{% endhint %}

#### Use Authentication.ps1

You can use the admin console to configure OpenID Connect. We recommend this method as you will not need to restart the PowerShell Universal service after configuring OIDC.

To add a new authentication method, navigate to Security \ Authentication and add the OpenID Connect provider.

![](<../../.gitbook/assets/image (462).png>)

Once the provider has been added, you can click the details button to enter the settings you'll need to authenticate against your OIDC provider. After setting the OIDC options, set the provider to enabled and log out. When visiting the `/admin` page, you'll be prompted for OIDC login.

<figure><img src="../../.gitbook/assets/image (238).png" alt=""><figcaption><p>OpenID Connect Settings</p></figcaption></figure>

### Delegated Access Tokens

You can use access tokens generated by an OIDC login for other services the user may have access to. Within your OIDC provider, like Entra ID, you can grant additional permissions to the token.

![](<../../.gitbook/assets/image (459).png>)

You will also have to enable access tokens within the authentication flow so that the token provides the necessary resource access.

![](<../../.gitbook/assets/image (270).png>)

Finally, within your PSU `appsettings.json` file, you will need to ensure that `SaveTokens` is enabled, the resource type includes token and the resource you wish to access is included in the Resource setting. The URL that you specify in the resource should be listed in within the provider.

The below example adds a resource for Microsoft O365.

```javascript
    "OIDC": {
  "Enabled": "true",
  "CallbackPath": "/auth/signin-oidc",
  "ClientID": "<clientID>",
  "ClientSecret": "<clientSecret>",
  "Resource": "https://manage.office.com/",
  "Authority": "https://login.microsoftonline.com/tenant",
  "ResponseType": "id_token token",
  "SaveTokens": "true",
  "UseTokenLifetime": true
},
```

Within your dashboard, you will now have access to an `$AccessToken` and `$IdToken` variable that you can use with cmdlets that require authorization.

For example, the `Connect-AzureAd` cmdlet accepts an access token.

```powershell
Connect-AzureAD
       [-AzureEnvironmentName <EnvironmentName>]
       [-TenantId <String>]
       -AadAccessToken <String>
       [-MsAccessToken <String>]
       -AccountId <String>
       [-LogLevel <LogLevel>]
       [-LogFilePath <String>]
       [-InformationAction <ActionPreference>]
       [-InformationVariable <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

### Refresh Tokens

You can configure Azure Active Directory and PowerShell Universal to provide refresh tokens for requesting new tokens if the access token expires. To do so, you will need to enable offline\_access in your app registration.

<figure><img src="../../.gitbook/assets/image (2) (1) (2).png" alt=""><figcaption><p>offline_access</p></figcaption></figure>

When configuring PowerShell Universal, you need to request the `offline_access` scope and set SaveTokens to true and use the id\_token response type.

```json
"OIDC": {
    "Enabled": "true",
    "CallbackPath": "/auth/signin-oidc",
    "ClientID": "----",
    "ClientSecret": "---",
    "Resource": "https://graph.microsoft.com",
    "Authority": "https://login.microsoftonline.com/----",
    "ResponseType": "code id_token",
    "SaveTokens": "true",
    "CorrelationCookieSameSite": "",
    "UseTokenLifetime": true,
    "Scope": "openid profile groups offline_access",
    "GetUserInfo": false
},
```

Once configured, you can access the `$RefreshToken` variable in your scripts and apps.

## Configuring Okta

Okta supports OpenID Connect. You can configure an application to allow authentication against PowerShell Universal instances.

Within your Okta admin console, expand Applications and click Applications. Then click Create App Integration.

![](<../../.gitbook/assets/image (489).png>)

Select OIDC and Web Application.

![](<../../.gitbook/assets/image (373).png>)

Name your application and define the Sign-In redirect URL used to call your PowerShell Universal server. You will need to specify this callback URL within your PowerShell Universal configuration.

![](<../../.gitbook/assets/image (170).png>)

Once you've created your application, take note of your Client ID and Client Secret. You will specify these within your PowerShell Universal configuration.

![](<../../.gitbook/assets/image (306).png>)

Within the Sign On tab, specify the group claims filter to use for providing claims to PowerShell Universal. These claims can be used to assign roles based on group membership. The following filter returns all claims.

![](<../../.gitbook/assets/image (285).png>)

Once you have your Application configured, you can configure PowerShell Universal.

### Configurating Universal for Okta

Once you have defined your Okta application, you can set your `appsettings.json` file to use the provider for logins. Below is an example of the section required for Okta to function. Take note of the scope functionality as it is required for retrieving group membership.

```json
    "OIDC": {
      "Enabled": "true",
      "CallbackPath": "/authorization-code/callback",
      "ClientID": "6f006906-643a-40fe-af00-9060cea5d6ef",
      "ClientSecret": "M~.rE56.md_MOpB2I5kwj_voFuX-i891N0",
      "Resource": "",
      "Authority": "https://poshtools.okta.com",
      "ResponseType": "code",
      "SaveTokens": "true",
      "CorrelationCookieSameSite": "",
      "UseTokenLifetime": true,
      "Scope": "openid profile groups",
      "GetUserInfo": true
    },
```

### Role-Based Access

In order to look up group membership for Okta, you will need to use the `$UserInfo` variable that is available within `roles.ps1`. This variable provides additional information about the user logging in.

The groups property will contain a list of groups the user is a member of. You can validate membership by checking whether the list contains the desired group.

```powershell
param($User)

$UserInfo.groups -contains 'Administrators'
```

### Delegated Access Tokens

Access tokens are available for users within their scripts. You can use access tokens in jobs started by users and dashboards.

For example, you could return the current user's information by using the access token provided by Okta.

```powershell
Invoke-RestMethod https://poshtools.okta.com/oauth2/v1/userinfo -Headers @{
    Authorization = "Bearer $AccessToken"
}
```

## Viewing Claim Information

If you are unsure about what claim information is being sent to PowerShell Universal from your identity provider, you can use the View Claim Information button on the Security \ Roles page to view all the roles that have been provided to PSU from the remote system.
