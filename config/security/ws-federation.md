# WS-Federation

WS-Federation supports both Active Directory Federation Services and Azure Active Directory.

You first need to configure ADFS or AzureAD to support Universal.

### Configuring ADFS for Universal <a id="configuring-adfs-for-universal-dashboard"></a>

#### Service Settings <a id="service-settings"></a>

These are the current Federation Service settings for our domain.![](https://gblobscdn.gitbook.com/assets%2F-L9mVQO4zbOX7ZcHvIte%2F-Lob6ow15SQRLl3vo8ZV%2F-Lob7luBvuEGUTrLIors%2Fimage.png?alt=media&token=64c3c00f-1d2c-4346-bcc1-dd89e7cf4c24)

#### Relying Parties <a id="relying-parties"></a>

You need to configure the following Relying Parties settings for Universal. On the Identifiers tab, provide the URL to the Universal website. HTTPS is required.

![](https://gblobscdn.gitbook.com/assets%2F-L9mVQO4zbOX7ZcHvIte%2F-Lob6ow15SQRLl3vo8ZV%2F-Lob8DOuN3sGBzbdctQb%2Fimage.png?alt=media&token=8b2fac2f-c5e1-4ceb-963e-ab9c7eb85484)

On the Endpoints tab. You'll need to include a WS-Federation Passive Endpoint. Make sure to include the trailing slash.

![](https://gblobscdn.gitbook.com/assets%2F-L9mVQO4zbOX7ZcHvIte%2F-Lob6ow15SQRLl3vo8ZV%2F-Lob8hIg0Ot1uN1PsimG%2Fimage.png?alt=media&token=e6673c7c-a125-4b04-b0c0-ba7d0a677d6a)

Finally, you'll need to configure a Claim Issuance Policy for the Relying Party Trust. Create an Issuance Transform Rule that sends at least the Name and Name ID to Universal.![](https://gblobscdn.gitbook.com/assets%2F-L9mVQO4zbOX7ZcHvIte%2F-Lob6ow15SQRLl3vo8ZV%2F-Lob92zcF4qYpWtR0g_4%2Fimage.png?alt=media&token=34dfd4db-d742-4f8b-a271-86d37542dc35)

You can configure additional claims you'd like to use if you are using policies in Universal. 

### Configuring For Azure Active Directory <a id="configuring-for-azure-active-directory"></a>

Follow the documentation for the Azure Active Directory configuration found on this [Microsoft Document](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/ws-federation?view=aspnetcore-2.2#azure-active-directory).

### Configuring Universal <a id="configuring-universal-dashboard"></a>

After configuring ADFS or AAD, you can now provide the properties to Universal for the MetadataAddress and Wtrealm. Read about these settings on the our [Settings ](../settings.md)page. 

```text
$Authentication = New-UDAuthenticationMethod -MetadataAddress 'https://ironman.local:443/FederationMetadata/2007-06/FederationMetadata.xml' -Wtrealm https://ironman.local:12345$LoginPage = New-UDLoginPage -AuthenticationMethod $Authentication
```

When running your server, you should now be prompted for your credentials either via the Internet Explorer single-sign system or you will be forwarded to the WS-Fed login page.![](https://gblobscdn.gitbook.com/assets%2F-L9mVQO4zbOX7ZcHvIte%2F-Lob6ow15SQRLl3vo8ZV%2F-Lob9yeDdGENbUiyz4Sj%2Fimage.png?alt=media&token=910db2dd-85f3-46eb-b3ec-9f551f244439)

