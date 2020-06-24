---
description: Configure OpenID Connect with Universal.
---

# OpenID Connect

OpenID Connect is an authentication layer on top of OAuth 2.0, an authorization framework. It is supported by many vendors and provides the ability to authenticate against systems like AzureAD. 

This document will outline the steps necessary to configure AzureAD OpenID Connect and use it with Universal. 

## Configuring AzureAD

Within the Azure Portal, navigate to your Azure Active Directory blade. Next, click the App registrations node and then click New registration.

![](../../.gitbook/assets/image%20%2830%29.png)

In the New registration page, enter the name of your application and the reply URL. The URL can be configured in the `appsettings.json` for Universal but the default value is shown below. 

![](../../.gitbook/assets/image%20%2833%29.png)

Next, you'll need to configure a client secret. You can click the Certificates & secrets menu and then click New client secret. This secret will need to go into the `appsettings.json` file. 

![](../../.gitbook/assets/image%20%2829%29.png)

Now, you will need to take note of your Application \(client\) ID GUID. This will be used in the `appsettings.json` file. 

![](../../.gitbook/assets/image%20%2834%29.png)

Finally, you will have to click the Endpoints button to open the Endpoints drawer. This contains a list of the endpoints. Make note of the OAuth 2.0 authorization endpoint URL. You will need this for the `appsettings.json`.

![](../../.gitbook/assets/image%20%2832%29.png)

## Configuring Universal

Now that we have completed the configuration of an AzureAD App Registration, we can update the `appsettings.json` file with the appropriate settings. For my application, it would look something like this. 

```text
  "OIDC": {
      "Enabled": "true",
      "CallbackPath": "/auth/signin-oidc",
      "ClientID": "6f006906-643a-40fe-af00-9060ceffffff",
      "ClientSecret": "xxxxxxxxxxxxxxxxxx",
      "Resource": "",
      "Authority": "https://login.microsoftonline.com/fffffff-4b76-4470-a736-8481d7a2ed87",
      "ResponseType": "code",
      "SaveTokens": "false"
    },
```



