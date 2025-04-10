---
description: Enterprise security features for PowerShell Universal.
---

# Enterprise Security

PowerShell Universal provides enterprise security features to allow for integrating with existing authentication and authorization methods. It also includes fine grained Permissions that can restrict access the Admin Console for specific features.

Enterprise Security requires a [Server or Enterprise license](https://ironmansoftware.com/pricing/powershell-universal).

## Multiple Challege Schemes

When multiple challenge schemes are configured (e.g. SAML2 and Windows), then PowerShell Universal will select the first scheme that is defined in `authentication.ps1` . When access a protected resource, like an app or the admin console, the highest priority scheme will be used.&#x20;

The below example will use Windows authentication when access protected resources by default. If you wish to login with OpenID Connect, you would need to visit the login page and click the Login with OpenID Connect button.&#x20;

```powershell
Set-PSUAuthenticationMethod -Type 'Windows'
Set-PSUAuthenticationMethod -Type 'OpenIDConnect'
```
