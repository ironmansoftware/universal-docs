---
description: App tokens for accessing PowerShell Universal APIs.
---

# App Tokens

PowerShell Universal app tokens can be used with both [custom API endpoints](../api.md) and the [management API](../management-api.md). The management API uses the standard Administrator, Operator and Reader roles. The custom API app tokens can utilize custom roles as well as the built in ones.

You can grant App Tokens to using the Admin Console or you can use the Management API directly.

## Admin Console

To grant a token in the Admin Console, navigate to Security \ Tokens. Click the Add New App Token button to grant an App Token.

![](<../../.gitbook/assets/image (375) (1) (1) (1) (1) (1).png>)

When you click Grant App Token, you will be provided with a dialog that allows you to specify the Identity, Role and expiration time of the token.

![App Token options.](<../../.gitbook/assets/image (168).png>)

## Management API

You can also grant app tokens to users from the management API. To grant an App Token programmatically using the API, you can do the following.

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

Administrators can grant app tokens to any user by specifying the user's identity ID. In order to grant an app token to an identity via the REST API, the user needs to have a defined role. The user is defined with the Operator role and thus their App Token will be granted access based on that role.

![](<../../.gitbook/assets/image (80).png>)

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

## Migrating App Tokens

You can migrate app tokens between systems by using the management API. This is helpful when developing for high availability scenarios.

The following is an example of the POST that is required to create an existing app token in any PSU instance. Note that the signing key must be the same between the instances. You need a valid app token in the target system to create the migrated tokens.

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

When enhanced app token security is enabled, token values are only accessible once they are created. They are hashed and the hash value is stored in the database rather than the token. You will use the token the same way as any other token.&#x20;
