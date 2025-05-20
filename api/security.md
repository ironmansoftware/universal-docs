---
description: Authentication and authorization for REST APIs.
---

# Security

Once enabled, you will be able to enforce authentication and authorization on your endpoints.

## Defining Secure Endpoints

You can define secure endpoints in the UI by enabling authentication. You will endpoint authentication and authorization under the Security tab of an endpoint's properties.

You can also define secure endpoints using the `.universal/endpoints.ps1` file or the Management API using `New-PSUEndpoint`.

```powershell
New-PSUEndpoint -Url '/endpoint' -Method 'GET' -Endpoint {
   "Hello, world!"
} -Authentication
```

When authentication is enabled, it will enforce the use of one of the configured authentication methods. APIs support the following methods.

* JWT App Tokens
* Windows Authentication
* Cookie Authentication
* Basic Authentication

## Accessing Secure Endpoints

Once you have defined a secure endpoint, you will need to provide authentication and authorization to access the endpoint.

### Authenticating with tokens

{% hint style="warning" %}
Note that if you are hosting in IIS and do not have Anonymous Authentication enabled, you will not be able to pass app tokens to the PowerShell Universal server.
{% endhint %}

To authenticate with tokens, first, you need generate a new app token for use. You can use the `Grant-PSUAppToken` cmdlet to do so remotely or you can create an app token in the UI using the Settings Security AppTokens tab.

Hover over your user name in the top right of the admin console, click Tokens and click Create Application Token.&#x20;

Once you have created your app token, you can now use it to authenticate against the secure endpoint. To do so, pass the Authorization header along with the request.

```powershell
Invoke-RestMethod http://localhost:5000/auth -Headers @{ Authorization = "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiQWRtaW4iLCJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9oYXNoIjoiMWUyY2IzNzAtMmMyNS00ZDU5LTk4YzgtMzc5MTFjMDAyZmI5Iiwic3ViIjoiUG93ZXJTaGVsbFVuaXZlcnNhbCIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6IkFkbWluaXN0cmF0b3IiLCJuYmYiOjE2MDU2NjEyNTUsImV4cCI6MTYzNzM2NzI1OCwiaXNzIjoiSXJvbm1hblNvZnR3YXJlIiwiYXVkIjoiUG" }
```

#### Custom Authorization Header

PowerShell Universal provides a custom authorization header to support scenarios with reverse proxies that may require their own Authorization header. If the `X-PSU-Authorization` header is specified, PSU will ignore the `Authorization` header and use this header instead.&#x20;

```
Invoke-RestMethod http://localhost:5000/auth -Headers @{ 
    Authorization = "Bearer msft_xyz_123" 
    'X-PSU-Authorization' = 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiQWRtaW4iLCJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9oYXNoIjoiMWUyY2IzNzAtMmMyNS00ZDU5LTk4YzgtMzc5MTFjMDAyZmI5Iiwic3ViIjoiUG93ZXJTaGVsbFVuaXZlcnNhbCIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6IkFkbWluaXN0cmF0b3IiLCJuYmYiOjE2MDU2NjEyNTUsImV4cCI6MTYzNzM2NzI1OCwiaXNzIjoiSXJvbm1hblNvZnR3YXJlIiwiYXVkIjoiUG'
}
```

### Authenticating with Windows Authentication

To authenticate with [Windows Authentication](../config/security/#windows-authentication-in-iis), you can use the `-UseDefaultCredentials` parameter of `Invoke-RestMethod` and `Invoke-WebRequest` . This will perform negotiate authentication whether you are running inside IIS or a service.

```powershell
Invoke-RestMethod http://localhost:5000/auth -UseDefaultCredentials
```

### Authenticating with Cookies

To authenticate with cookies, you will first need to call the login API to receive a valid cookie from the system. You can use `Invoke-WebRequest` to do so. Pass the user name and password as the body. Specify the `-SessionVariable` parameter to establish a session.

```powershell
Invoke-WebRequest http://localhost:5000/api/v1/signin -Body (@{ 
    UserName = "Admin"
    Password = "Any"
} | ConvertTo-Json) -ContentType 'application/json' -SessionVariable mySession -Method POST
```

Once you have successfully authenticated, you can use your `$mySession` variable to call secure endpoints.

```powershell
 Invoke-WebRequest http://localhost:5000/auth -WebSession $mySession
```

## Enforcing Roles

In addition to creating endpoints that require authentication, you can also enforce roles by define a role in the `New-PSUEndpoint` cmdlet or by selecting one in the UI. If a role is selected, it's possess the role.

Windows and Cookie authentication will assign roles based on the Identity of the user and the role policies as they are applied.

JWT app tokens will use the role that was defined when they were generated.

## API

* [New-PSUEndpoint](../cmdlets/New-PSUEndpoint.txt)
* [Get-PSUEndpoint](../cmdlets/Get-PSUEndpoint.txt)
* [Remove-PSUEndpoint](../cmdlets/Remove-PSUEndpoint.txt)
* [New-PSUApiResponse](../cmdlets/New-PSUApiResponse.txt)
* [Set-PSUSetting](../cmdlets/Set-PSUSetting.txt)
