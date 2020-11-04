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



