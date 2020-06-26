# Management API

You can manage PowerShell Universal using the built in Management API. It provides the ability to perform all the actions as the admin console in an automated manner. You can view and test the API by visiting the Swagger API documentation at it's default location on your machine `http://localhost:5000/swagger/index.html` . 

{% hint style="info" %}
The Management API is built in and does not require a license to Universal API. 
{% endhint %}

## PowerShell Module

We provide a PowerShell module that calls the API on your behalf so you do not have to write the HTTP requests yourself. You can download this module from the PowerShell Gallery.

```text
Install-Module Universal
```

The PowerShell module requires an app token and computer name to call the Universal server. You can provide this items on each call. 

```text
Invoke-UAScript -Script $Script -ComputerName http://localhost:5000 -AppToken $AppToken
```

Additionally, you can connect to the Universal server using `Connect-UAServer`.

```text
Connect-UAServer -ComputerName http://localhost:5000 -AppToken $AppToken
```

## App Tokens

To call the management API, you will need to grant an App Token to your users. You can grant App Tokens to using the Admin Console or you can use the Management API directly. 

### Admin Console

To grant a token in the Admin Console, navigate to Settings \ Security \ AppTokens. Click the Grant App Token button to grant an App Token for the current user. 

![](../.gitbook/assets/image%20%2883%29.png)

### Management API

You can also grant app tokens to users from the management API. To grant an App Token programmatically using the API, you can do the following. 

```text
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

![](../.gitbook/assets/image%20%2884%29.png)

```text
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

