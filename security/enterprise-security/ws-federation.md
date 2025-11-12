# WS-Federation

{% hint style="info" %}
WS-Federation requires a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

WS-Federation supports both Active Directory Federation Services and Azure Active Directory.

You first need to configure ADFS or AzureAD to support Universal.

## Configuring ADFS for Universal <a href="#configuring-adfs-for-universal-dashboard" id="configuring-adfs-for-universal-dashboard"></a>

### Service Settings <a href="#service-settings" id="service-settings"></a>

First, you will need to gather the Federation Service Properties from ADFS. Open the AD FS app (Microsoft.IdentityServer.msc). Next, click Service and then Edit Federation Service Properties.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

This will open a dialog with the values for your ADFS service. You will need these values for configuring PowerShell Universal.

![](https://gblobscdn.gitbook.com/assets%2F-L9mVQO4zbOX7ZcHvIte%2F-Lob6ow15SQRLl3vo8ZV%2F-Lob7luBvuEGUTrLIors%2Fimage.png?alt=media\&token=64c3c00f-1d2c-4346-bcc1-dd89e7cf4c24)

### Relying Parties <a href="#relying-parties" id="relying-parties"></a>

If you have no Reply Party Trusts configured, click Add Replying Party Trust. Select Claims aware.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Claims Aware</p></figcaption></figure>

Select Enter data about the relying party manually.

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>Manual Relying Party</p></figcaption></figure>

Specify a name for the relying party.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Relying Party Name</p></figcaption></figure>

Enable WS-Federation Passive protocol. Enter the PowerShell Universal server URL with a trailing slash.

<figure><img src="../../.gitbook/assets/image (268).png" alt=""><figcaption></figcaption></figure>

Enter the URL of your PowerShell Universal server.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Replying Party Trust Identifier</p></figcaption></figure>

After finishing your Replying Party Trust configuration, you will need to setup a Claim Issuance Policy. Create an Issuance Transform Rule that sends at least the Name and Name ID to Universal.

<figure><img src="https://gblobscdn.gitbook.com/assets%2F-L9mVQO4zbOX7ZcHvIte%2F-Lob6ow15SQRLl3vo8ZV%2F-Lob92zcF4qYpWtR0g_4%2Fimage.png?alt=media&#x26;token=34dfd4db-d742-4f8b-a271-86d37542dc35" alt=""><figcaption></figcaption></figure>

You can configure additional claims you'd like to use if you are using policies in Universal.

### Troubleshooting

MSIS7065: There are no registered protocol handlers on path /adfs/ls to process the incoming request.

This issue can be caused if the IDP Initiated Sign On page is disabled. This is the default. Run the following command from an administrative console.

```powershell
 Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
```

MSIS7001: The passive protocol context was not found or not valid. If the context was stored in cookies, the cookies that were presented by the client were not valid. Ensure that the client browser is configured to accept cookies from this website and retry this request.

## Configuring For Azure Active Directory <a href="#configuring-for-azure-active-directory" id="configuring-for-azure-active-directory"></a>

Follow the documentation for the Azure Active Directory configuration found on this [Microsoft Document](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/ws-federation?view=aspnetcore-2.2#azure-active-directory).

## Configuring Universal <a href="#configuring-universal-dashboard" id="configuring-universal-dashboard"></a>

### Use Appsettings.json

After configuring ADFS or AAD, you can now provide the properties to Universal for the MetadataAddress and Wtrealm. Read about these settings on the our [Settings ](../../config/settings.md)page.

Here is an example of how to update the `appsettings.json` file to accommodate the correct settings for WS-Federation.

```javascript
{
  "Kestrel": {
    "Endpoints": {
      "HTTP": {
        "Url": "http://*:5000"
      }
    },
    "RedirectToHttps": "false"
  },
  "ApplicationInsights": {
    "InstrumentationKey": ""
  },
  "Logging": {
    "Path": "%PROGRAMDATA%/PowerShellUniversal/log.txt",
    "RetainedFileCountLimit": 31,
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*",
  "CorsHosts": "",
  "Data": {
    "RepositoryPath": "%ProgramData%\\UniversalAutomation\\Repository",
    "ConnectionString": "%ProgramData%\\UniversalAutomation\\database.db",
    "GitRemote": "",
    "GitUserName": "",
    "GitPassword": "", 
    "ConfigurationScript": ""
  },
  "Api": {
    "Url": ""
  },
  "Authentication" : {
    "Windows": {
      "Enabled": "false"
    },
    "WSFed": {
        "Enabled": "true",
        "MetadataAddress": "https://ironman.local:443/FederationMetadata/2007-06/FederationMetadata.xml",
        "Wtrealm": "https://ironman.local:12345",
        "CallbackPath": "/auth/signin-wsfed"
    },
    "OIDC": {
      "Enabled": "false",
      "CallbackPath": "/auth/signin-oidc",
      "ClientID": "",
      "ClientSecret": "",
      "Resource": "",
      "Authority": "",
      "ResponseType": "",
      "SaveTokens": "false"
    },
    "SessionTimeout": "25"
  },
  "Jwt": {  
    "SigningKey": "PleaseUseYourOwnSigningKeyHere",  
    "Issuer": "IronmanSoftware",
    "Audience": "PowerShellUniversal"
  },
  "UniversalDashboard": {
    "AssetsFolder": "%ProgramData%\\PowerShellUniversal\\Dashboard"
  },
  "ShowDevTools": false,
  "HideAdminConsole": false
}
```

When running your server, you should now be prompted for your credentials either via the Internet Explorer single-sign system or you will be forwarded to the WS-Fed login page.

![](https://gblobscdn.gitbook.com/assets%2F-L9mVQO4zbOX7ZcHvIte%2F-Lob6ow15SQRLl3vo8ZV%2F-Lob9yeDdGENbUiyz4Sj%2Fimage.png?alt=media\&token=910db2dd-85f3-46eb-b3ec-9f551f244439)

### Use Authentication.ps1

You can configure WS-Federation authentication in the admin console. To do so, navigate to Security \ Authentication. Add the WS-Federation provider by selecting it from the drop down in the top right.

![](<../../.gitbook/assets/image (462).png>)

Next, edit the properties of the authentication provider and specify the configuration details for your ADFS setup.

![](<../../.gitbook/assets/image (232).png>)

Once configured, enable the WS-Federation provider. Then, log out and navigate to `/admin` You will be prompted to login to your WS-Federation provider.
