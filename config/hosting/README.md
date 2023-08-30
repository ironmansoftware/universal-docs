# Hosting

You can host PowerShell Universal as a Windows Service, in IIS, as a Azure Web App or just as a stand alone application. If you are running on Windows, we suggest either a Windows Service or IIS.

## Hosting as a Windows Service

To host as a Windows Service, you can download and install the PowerShell Universal MSI. The MSI will automatically install the PowerShell Universal service and start it. Jobs will run under the system account by default but you can configure the service to run under another account after installation.

After the MSI has finished setup, your default web browser will open to [http://localhost:5000](http://localhost:5000) for login. The default login credentials are set to Admin and any password.

### Configuring a Windows Service Manually

You do not need to use the MSI to configure Universal as a Windows Service. You can also do it manually with the following PowerShell script.

```powershell
New-Service -Name "PowerShellUniversal" -BinaryPathName "Universal.Server.exe --service" -Description "PowerShell Universal server service." -DisplayName "PowerShell Universal" -StartupType Automatic
Start-Service PowerShellUniversal
```

## Hosting in Azure

Read our [Azure hosting guide](azure.md).

## Hosting Manually

You can also host the Universal server as a stand alone application. Simply run the `Universal.Server.exe` from the binary directory to utilize the [Kestrel web server implementation in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1) to start the web server.

## Web Server Configuration

{% hint style="info" %}
This section applies to Universal when it is hosted outside of IIS.
{% endhint %}

### Setting the Port and Listening Address

You can set the port of the Universal server by modifying the `appsettings.json` file. We recommend that you create an `appsettings.json` file in the [default configuration folder](https://docs.ironmansoftware.com/config/settings).

**Windows**

`%ProgramData%\PowerShellUniversal`

**Linux**

`%HOME%/.PowerShellUniversal`

To set the port, change the Kestrel endpoints section of the `appsettings.json`. By default, the configuration is defined to listen on port 5000 and on any address.

```javascript
    "Kestrel": {
    "Endpoints": {
      "HTTP": {
        "Url": "http://*:5000"
      }
    }
  },
```

### Configuring HTTPS

To configure HTTPS, you can adjust the `appsettings.json` file to use a particular certificate and port. The below configuration uses the `testCert.pfx` file and `testPassword` and listens on port 5463.

#### PFX Certificates

```javascript
{
  "Kestrel": {
    "Endpoints": {
       "HTTP": { "Url": "http://*:5000" },
           "HTTPS": {
              "Url": "https://*:5463",
              "Certificate": {
                  "Path": "testCert.pfx",
                  "Password": "testPassword"
              }
          }
    }
}
```

#### Certificate Store

To configure a certificate in a particular location and store, you can use a configuration such as this. When selecting the certificate by subject name, ensure you use the common name with out `CN=` prefix.&#x20;

```javascript
{
  "Kestrel": {
    "Endpoints": {
      "HTTPS": {
         "Url": "https://*:443",
           "Certificate": {
             "Subject": "windows-server.ironman.local",
             "Store": "My",
             "Location": "LocalMachine",
             "AllowInvalid": "true"
           }
      }
   }
}
```

Location can be either `CurrentUser` or `LocalMachine`.

#### Certificate Store by Thumbprint

You can use thumbprint rather than subject in version 3.4 and later.&#x20;

```powershell
{
  "Kestrel": {
    "Endpoints": {
      "HTTPS": {
         "Url": "https://*:443",
           "Certificate": {
             "Thumbprint": "SDFSDFSDFSDFSDFSDFSDFFSD",
             "Store": "My",
             "Location": "LocalMachine",
             "AllowInvalid": "true"
            }
         }
      }
   }
}
```

#### PEM And Key Certificates

Some providers, like Let's Encrypt and GoDaddy, will issue certificates as PEM and key text files. You can use these types of certificates directly with the Kestrel web server. You will need to specify the `HttpsFromPem` section within the `Endpoints` for Kestrel.&#x20;

```json
{
  "Kestrel": {
    "Endpoints": {
      "HTTP": {
        "Url": "http://*:5000"
      },
      "HttpsFromPem": {
        "Url": "https://*:5001",
        "Certificate": {
          "Path": "C:\\Users\\adamr\\Desktop\\cert.pem",
          "KeyPath": "C:\\Users\\adamr\\Desktop\\key.pem"
        }
      }
    },
    "RedirectToHttps": "true"
  },
}
```

### Protocol

By default, Universal will listen on HTTP1 and HTTP2. You can adjust the protocols that the server listens to by setting the Protocols property. For example, you can specifically set HTTP1 and HTTP2 support with the following setting.

```javascript
"Kestrel": {
  "Endpoints": {
    "HTTP": {
      "Url": "http://*:5000",
      "Protocols": "Http1AndHttp2"
    }
  },
  "RedirectToHttps": "false"
},
```

Some versions of Windows Server (like 2012R2), do not support HTTP2. To disable HTTP2 support, set the listener to only listen on HTTP1.

```javascript
"Kestrel": {
  "Endpoints": {
    "HTTP": {
      "Url": "http://*:5000",
      "Protocols": "Http1"
    }
  },
  "RedirectToHttps": "false"
},
```

For a full set of listening options, you can refer to the [ASP.NET Core Documentation](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-3.1#listenoptionsusehttps).

## Example: Self-Signed Certificate&#x20;

In this example, we'll show how to create a self-signed certificated and use it with PowerShell Universal.&#x20;

First, create a self-signed certificate and store it into your local machine store. You will need to run PowerShell as administrator. The local machine store is required because PowerShell Universal may be running as service and not as your account.&#x20;

```powershell
New-SelfSignedCertificate -DnsName localhost -CertStoreLocation cert:\LocalMachine\My
```

Next, you'll need to configure PowerShell Universal to use the certificate. This can be accomplished by editing or creating the `appsettings.json` file in `%ProgramData%\PowerShellUniversal`. This file should already exist if you installed with the MSI installer. The contents of the file should include the DNS name of your certificate and the location.&#x20;

For self-signed certificates, you will need to include the `AllowInvalid` option.&#x20;

```json
{
  "Kestrel": {
    "Endpoints": {
      "HTTPS": {
         "Url": "https://*:443",
           "Certificate": {
             "Subject": "localhost",
             "Store": "My",
             "Location": "LocalMachine",
             "AllowInvalid": "true"
           }
      }
   }
}
```

Once you have updated the `appsettings.json` file, restart the PowerShell Universal service. You should now be able to access your PowerShell Universal web site at `https://localhost`.
