---
description: App tokens for accessing PowerShell Universal APIs.
---

# App Tokens

You can use PowerShell Universal app tokens with both [custom API endpoints](broken-reference/) and the [management API](../management-api.md). The management API uses the standard Administrator, Operator and Reader roles. The custom API app tokens can utilize custom roles as well as the built-in ones.

You can grant App Tokens to using the Admin Console or you can use the Management API directly.

## Admin Console

To grant a token in the Admin Console, navigate to Security \ Tokens. Click the Create App Token button to grant an App Token.

<figure><img src="../../.gitbook/assets/image (224) (1).png" alt=""><figcaption></figcaption></figure>

When you click Create App Token, a dialog allows you to specify the Identity, Role and expiration time of the token.

<figure><img src="../../.gitbook/assets/image (234).png" alt=""><figcaption><p>App Token Dialog</p></figcaption></figure>

## Management API

You can also grant app tokens to users from the management API. To grant an App Token programmatically using the API, you can do the following:

```
PS C:\Users\adamr> Invoke-RestMethod http://localhost:5000/api/v1/signin -Method POST -Body (@{ username = 'admin'; password = 'test' } | ConvertTo-Json) -SessionVariable Session -ContentType 'application/json'
PS C:\Users\adamr> Invoke-RestMethod http://localhost:5000/api/v1/apptoken/grant  -WebSession $Session

id          : 3
token       : eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2Ns
              YWltcy9uYW1lIjoiYWRtaW4iLCJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9oYXNoI
              joiYjJlOGM4MDktMjE0NS00NjhhLWI4NTEtYjU0MjVhZDgzOTQ2Iiwic3ViIjoiUG93ZXJTaGVsbFVuaXZlcnNhbCIsImh0dHA6Ly9zY2
              hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6WyJBZG1pbmlzdHJhdG9yIiwiT3BlcmF0b3I
              iLCJSZWFkZXIiXSwibmJmIjoxNTkzMTkyMjY1LCJleHAiOjE2MjQ3MjgyNjUsImlzcyI6Iklyb25tYW5Tb2Z0d2FyZSIsImF1ZCI6IlBv
              d2VyU2hlbGxVbml2ZXJzYWwifQ.hnKyXe8C4kbrmkeeUFr-LUDjVr-xP7fRWwgClcrnxfc
identity    : @{id=3; name=admin; source=0; role=}
revoked     : False
role        : Administrator, Operator, Reader
created     : 26/06/2020 17:24:25
expiration  : 26/06/2021 17:24:25
revokedDate : 01/01/0001 00:00:00
```

Administrators can grant app tokens to any user by specifying the user's identity ID. To grant an app token to an identity via the REST API, the user needs a defined role. The Operator role defines the user, and their App Token will be granted access based on that role.

```
PS C:\Users\adamr> Invoke-RestMethod http://localhost:5000/api/v1/apptoken/grant/2  -WebSession $Session

id          : 4
token       : eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2Ns
              YWltcy9uYW1lIjoiYWRhbUBpcm9ubWFuc29mdHdhcmUub25taWNyb3NvZnQuY29tIiwiaHR0cDovL3NjaGVtYXMueG1sc29hcC5vcmcvd
              3MvMjAwNS8wNS9pZGVudGl0eS9jbGFpbXMvaGFzaCI6IjhhYWM2NWFmLTA2NmItNDYwNy1hMGJjLTNlYTM2ZDY2YjJmMSIsInN1YiI6Il
              Bvd2VyU2hlbGxVbml2ZXJzYWwiLCJodHRwOi8vc2NoZW1hcy5taWNyb3NvZnQuY29tL3dzLzIwMDgvMDYvaWRlbnRpdHkvY2xhaW1zL3J
              vbGUiOiJPcGVyYXRvciIsIm5iZiI6MTU5MzE5MjM2MCwiZXhwIjoxNjI0NzI4MzYwLCJpc3MiOiJJcm9ubWFuU29mdHdhcmUiLCJhdWQi
              OiJQb3dlclNoZWxsVW5pdmVyc2FsIn0.9VYiRFOojFyZMH0E5rwdfFcOkoasXFrrWJDNtYk0PIw
identity    : @{id=2; name=adam@ironmansoftware.onmicrosoft.com; source=0; role=}
revoked     : False
role        : Operator
created     : 26/06/2020 17:26:00
expiration  : 26/06/2021 17:26:00
revokedDate : 01/01/0001 00:00:00
```

## Roles

App Tokens roles are assigned directly into the token itself. Roles indicate what the token is capable of performing. They are not calculated during use so role to claim mapping will not work with app tokens.

We also suggest limiting the number of roles within an app token. The more roles that are added to the token will increase the size of the token and reduce performance or cause issues with certain tools that do not allow for longer token values.

You can use custom roles with a custom set of permissions to limit the number of roles but to provide custom access to the PowerShell Universal platform. Permissions are evaluated when the role is used. This means that assigning a custom role to a token makes it more flexible than a built-in role since the permissions can be add or removed from a role without generating a new token.

## Migrating App Tokens

You can migrate app tokens between systems using the management API. This is helpful when developing for high availability scenarios.

The following is an example of the POST required to create an existing app token in any PSU instance. Note that the signing key must be the same between the instances. You need a valid app token in the target system to create the migrated tokens.

```powershell
Invoke-RestMethod http://localhost:5000/api/v1/apptoken -Method POST -Body (@{
        Token      = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiQWRtaW4iLCJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9oYXNoIjoiMDhiYTFlMTktMjgyZi00YTRjLWIxZGUtNTY0Zjk3NWU2ODEwIiwic3ViIjoiUG93ZXJTaGVsbFVuaXZlcnNhbCIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6InBvbGljeSIsIm5iZiI6MTYzMzEwNjkzMywiZXhwIjoxNjQwODg2NDgwLCJpc3MiOiJJcm9ubWFuU29mdHdhcmUiLCJhdWQiOiJQb3dlclNoZWxsVW5pdmVyc2FsIn0.GHjJI3kMpcAY1pvOGLWOdPqC2-IPo0-4lJfHZwStmOk'
        Identity   = @{
            Name = 'Admin'
        }
        Role       = 'Administrator'
        Expiration = (Get-Date).AddMonths(6)
    } | ConvertTo-Json) -Headers @{
    "Content-Type"  = "application/json";
    "Authorization" = "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiQWRtaW4iLCJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9oYXNoIjoiMjVjMzFlZTAtMGM4Mi00NzBiLWJkZGYtOGFmOTgxZGI2ZDdmIiwic3ViIjoiUG93ZXJTaGVsbFVuaXZlcnNhbCIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6IkFkbWluaXN0cmF0b3IiLCJuYmYiOjE2MzM2NDY5OTgsImV4cCI6MTYzNjIzODk0MCwiaXNzIjoiSXJvbm1hblNvZnR3YXJlIiwiYXVkIjoiUG93ZXJTaGVsbFVuaXZlcnNhbCJ9.jw2VCvtpOWpgnpIUlO8sTdK9Z5RMoWLmvYn0MDmzkNM"   
}
```

## Enhanced App Token Security

When enhanced app token security is enabled, token values are only accessible upon creation. They are hashed and the database stores the hash value rather than the token. You use the token the same way as any other token.

{% hint style="warning" %}
Enabling app token security will invalidate all existing tokens.
{% endhint %}

## System Tokens

System tokens are a way to provide tokens to non-user systems. They are not tied directly to a user's identity. You can provide a name for the token as well as expiration and roles.

## Signing Keys

### Local Signing Key

By default, PowerShell Universal creates a signing key based on the Jwt \ SigningKey string in appsettings.json. This value is used to encode and decode the token. If the signing keys do not match, the token will be considered invalid. Changing the signing key will invalidate all existing signing keys.

### Remote Signing Key

You may want to use an OAuth 2.0 discovery document to provide signing key validation. By using a remote system such as this, you can ensure that when signing keys are changed, the PowerShell Universal configuration will not need to be changed. To use a remote signing key, set the Jwt \ DiscoveryDocument value in appsettings.json to the URL of the OAuth 2.0 meta data document. When PowerShell Universal loads, it will read the signing keys from the document and provide them to the JWT validation system.

```json
{
    "Jwt" : {
        "DiscoveryDocument": "https://auth20/metadata.xml"
    }
}
```

## External App Tokens

When configuring a remote signing key, tokens are then generated by the OAuth 2.0 provider. Because of this, claims information is also generated by that provided. In order to properly assign roles and permissions within PowerShell Universal, you will need to ensure that the proper claims are defined within the token. PowerShell Universal will evalute the following claim values within a token.

* PSUPermission - Defines the permissions of the token
* Roles - Defines the roles of the token.

In order to allow for access to resources within a PowerShell Universal instance, ensure that token contains the proper claims. For example, the following token would allow all access to PowerShell Universal management APIs because it provides the `PSUPermission` claim with a selector for all permissions. You can use the [example below](app-tokens.md#example-auth0-access-token-with-custom-claims) to see how to accomplish this in Auth0.

```json
{
  "PSUPermission": "(.*)",
  "iss": "https://myprovider.us.auth0.com/",
  "sub": "wKeaTMprlv7kX46eI9SwwvaGJzWPkbtt@clients",
  "aud": "https://mydomain.com",
  "iat": 1758898719,
  "exp": 1758985119,
  "scope": "(.*) Administrator",
  "gty": "client-credentials",
  "azp": "wKeaTMprlv7kX46eI9SwwvaGJzWPkbtt",
  "permissions": [
    "(.*)",
    "Administrator"
  ]
}
```

Alternatively, you can enable claims evaluation for JWT tokens. By default, PowerShell Universal uses a static set of permissions when receiving a token. If you enable claims evaluation for JWT tokens, the authorization system will process the token and add the permissions when the token is used rather than when it is generated.

### Claim Evaluation for Tokens

To enable Claim Evaluation for Tokens, you can adjust appsettings.json to instruct PSU to run claims evaluation during execution of the token validation.

```json
{
    "Jwt": {
        "EvaluateClaims": "true"
    }
}
```

This will use `roles.ps1` to check the claims of the tokens that are being provided and assign permissions based on the qualified roles.

### Example: Auth0 Access Token with Claims Evaluation

Using standard Auth0 features, you can generate tokens that can then provide roles based on the claims of the token. This does not require any special triggers or actions within Auth0.

#### Create an Auth0 Application

In Auth0, create an application for a regular web application. You can do so by clicking Applications \ Applications and then Create Application.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

#### Create an Auth0 API

Next, create an Auth0 API by clicking Applications \ APIs and then Create API. Set the name and namespace to unique values and leave the rest of the options as default.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### Create Custom Permission Scopes in your API

Within your API, define custom permissions, such as one with a Role name.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

#### Authorize the Application to Use the API

Within the Application settings, click APIs and toggle the switch by the API to authorize the application to use the API. Select the permissions you would like to provide to the application. These will show up as permission claims in the token.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Retrieve an Access Token from Auth0

With the Application and API defined, you can now request an access token in Auth0. The `client_id` and `client_secret` values can be found on the Application Details page. The `audience` value should be the Identifier for you API.

```powershell
Invoke-RestMethod 'https://ironmansoftware.us.auth0.com/oauth/token' -Body @{
    client_id = "xyz123"
    client_secret = "xyz123"
    audience = "https://powershelluniversal.com"
    grant_type = "client_credentials"
} -Method POST
```

#### Configure PowerShell Universal

You will need to configure PowerShell Universal to use Auth0 as the JWT provider. You can do so by adjusting the appsettings.json file. These should include values from Auth0. The `DiscoveryDocument` will be part of your tenant and helps define data like the signing keys for the JWT tokens. The `Issuer` will be the URL of your tenant. The `Audience` will be your API's identifier.

```json
{
    "Jwt": {
        "DiscoveryDocument": "https://ironmansoftware.us.auth0.com/v2.0/.well-known/openid-configuration",
        "Issuer": "https://ironmansoftware.us.auth0.com/",
        "Audience": "https://powershelluniversal.com",
        "EvaluateClaims": "true"
    }
}
```

#### Configure a Role to Map to the Auth0 Permission

Finally, create a role that maps to the Auth0 permission. The following example checks that the API token has a permissions claim with the value of `Administrator` like we configured above. If so, the token is assigned the API Admin role which has all permissions within PowerShell Universal's management API.

```powershell
New-PSURole -Name "API Admin" -Permissions ".*" -ClaimType "permissions" -ClaimValue "Administrator"
```

#### Using an App Token with PowerShell Universal

Now that you have an Auth0 app token, you can use it just as you would with built-in app tokens.

```powershell
Invoke-RestMethod http://localhost:5000/api/v1/identity/my -Headers @{ Authorization = "tokenValue" }
```

### Example: Auth0 Access Token with Custom Claims

You can use Auth0 APIs and Applications to provide app tokens for PowerShell Universal.

#### Create an Auth0 Application

In Auth0, create an application for a regular web application. You can do so by clicking Applications \ Applications and then Create Application.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

#### Create an Auth0 API

Next, create an Auth0 API by clicking Applications \ APIs and then Create API. Set the name and namespace to unique values and leave the rest of the options as default.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### Authorize the Application to Use the API

Within the Application settings, click APIs and toggle the switch by the API to authorize the application to use the API.

#### Retrieve an Access Token from Auth0

With the Application and API defined, you can now request an access token in Auth0. The `client_id` and `client_secret` values can be found on the Application Details page. The `audience` value should be the Identifier for you API.

```powershell
Invoke-RestMethod 'https://ironmansoftware.us.auth0.com/oauth/token' -Body @{
    client_id = "xyz123"
    client_secret = "xyz123"
    audience = "https://powershelluniversal.com"
    grant_type = "client_credentials"
} -Method POST
```

#### Configure PowerShell Universal

You will need to configure PowerShell Universal to use Auth0 as the JWT provider. You can do so by adjusting the appsettings.json file. These should include values from Auth0. The `DiscoveryDocument` will be part of your tenant and helps define data like the signing keys for the JWT tokens. The `Issuer` will be the URL of your tenant. The `Audience` will be your API's identifier.

```json
{
    "Jwt": {
        "DiscoveryDocument": "https://ironmansoftware.us.auth0.com/v2.0/.well-known/openid-configuration",
        "Issuer": "https://ironmansoftware.us.auth0.com/",
        "Audience": "https://powershelluniversal.com"
    }
}
```

#### Using an App Token with PowerShell Universal

Now that you have an Auth0 app token, you can use it just as you would with built-in app tokens.

```powershell
Invoke-RestMethod http://localhost:5000/api/v1/identity/my -Headers @{ Authorization = "tokenValue" }
```

#### Optional: Define an Auth0 Action Trigger

When granting a new access token from Auth0, they will not contain the standard roles or permissions like built-in app tokens in PowerShell Universal. You can control this by defining a Custom Action and assigning it to the `credential-exchange` trigger.

Click Actions and then Library and Create Action and then Create Custom Action. Select the Password Reset / Post Challenge Trigger and name the action.

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Define the action by setting a custom claim for the `PSUPermission` claim type. This example simply provides all access to PowerShell Universal APIs. You can use event context to define which permissions are received based on the access token request.

```javascript
exports.onExecuteCredentialsExchange = async (event, api) => {
  api.accessToken.setCustomClaim("PSUPermission", "(.*)")
};
```

Next, add the action to the workflow trigger for `credential-exchange` by clicking Actions and then Triggers and then `credential-exchange.`

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Drag the Set Permissions action into the workflow.

Once this has been completed, you can generate a new token and access any API within PowerShell Universal.

```powershell
Invoke-RestMethod http://localhost:5000/api/v1/identity -Headers @{ Authorization = "tokenValue" }
```
