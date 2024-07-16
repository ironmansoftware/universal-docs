---
description: Client certificate authentication for PowerShell Universal.
---

# Client Certificate

Client certificate authentication ensures that client machines hold a particular certificate when connecting to PowerShell Universal. The certificate check is handled during the HTTP negotiation so it affects the entire webserver and cannot be configured per route.&#x20;

For detailed information about client certificate authentication in ASP.NET Core 5.0, you can visit the [Microsoft documentation here](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/certauth?view=aspnetcore-5.0).&#x20;

## Enable Client Certificate Authentication&#x20;

You will need to enable HTTPS hosting and turn on client certificate authentication. First, ensure that you have an HTTP certificate selected and you have set the `ClientCertificateMode` to `RequireCertificate`. These settings can be set within the appsettings.json file.&#x20;

```json
"Kestrel": {
  "Endpoints": {
    "HTTPS": {
      "Url": "https://*:5000",
      "ClientCertificateMode": "RequireCertificate",
      "Certificate": {
        "Subject": "localhost",
        "Store": "My",
        "Location": "LocalMachine",
        "AllowInvalid": "true"
      }
    }
  },
  "RedirectToHttps": "false"
},
```

Next, you will need to enable client certificate authentication.

```json
"ClientCertificate": {
  "Enabled": "true"
},
```

## Authorization

You can use the roles.ps1 file to evaluate the certificate provided by the client. This can be used to determine which roles the user will receive when connecting to PSU.&#x20;

To evaluate the properties that are available during authorization, you can serialize the `$user` variable provided to the role policy functions.&#x20;

```powershell
param($User)

$User | ConvertTo-Json | Out-File .\user.txt

$true
```

You will receive information about the certificate within the user object similar to below.

```json
{
  "Claims": [
    {
      "Type": "issuer",
      "Value": "CN=Cert1, OU=Cert2, O=Org, L=Scottsdale, S=Arizona, C=US",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "LOCAL AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/thumbprint",
      "Value": "8D2212B6EA170A33055A5",
      "ValueType": "http://www.w3.org/2001/XMLSchema#base64Binary",
      "Issuer": "LOCAL AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname",
      "Value": "CN=*.cert.com, OU=Domain Control Validated",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "LOCAL AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.microsoft.com/ws/2008/06/identity/claims/serialnumber",
      "Value": "009D21369",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "LOCAL AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/dns",
      "Value": "*.cert.com",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "LOCAL AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    },
    {
      "Type": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
      "Value": "*.cert.com",
      "ValueType": "http://www.w3.org/2001/XMLSchema#string",
      "Issuer": "LOCAL AUTHORITY",
      "Properties": "System.Collections.Generic.Dictionary`2[System.String,System.String]"
    }
  ],
  "Identity": {
    "Name": "*.cert.com"
  }
}

```

You can evaluate the the claims using the `HasClaim` method. The following is an example of checking the thumbprint of the certificate.&#x20;

```powershell
param($User)

$User.HasClaim('http://schemas.xmlsoap.org/ws/2005/05/identity/claims/thumbprint', '8D2212B6EA170A33055A5')
```
