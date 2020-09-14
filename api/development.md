---
description: Building APIs in VS Code.
---

# Development

The [Visual Studio Code extension for PowerShell Universal](https://marketplace.visualstudio.com/items?itemName=ironmansoftware.powershell-universal) provides integration for working with APIs. We recommend you also install the [PowerShell extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell). 

{% hint style="info" %}
The first time you activate the Visual Studio Code extension, it will download the latest version of PowerShell Universal and start the server on port 5000.
{% endhint %}

## Developing APIs

You can add APIs by using the admin console or through the editor in Visual Studio Code. 

To add an API in the Admin Console, you can visit `http://localhost:5000/admin/apis` and click Add Endpoint.

![](../.gitbook/assets/image%20%28124%29.png)

Once an `endpoints.ps1` file has been created, you can click the Open Endpoints.ps1 button within the API tree view to view the configuration file for APIs. 

![](../.gitbook/assets/image%20%28122%29.png)

The configuration file uses the Universal PowerShell cmdlets to define the endpoints within Universal. 

If you created a blank endpoint, it would look something like this.

```text
New-PSUEndpoint -Url "/test" -Endpoint { 
    # Enter your script to process requests.
}
```

If you edit the `endpoints.ps1` file, it will update the API automatically. For example, if I added a new API, it would then appear in the admin console. 

```text
New-PSUEndpoint -Url "/test" -Endpoint { 
 "hello"
}

New-PSUEndpoint -Url "/test2" -Endpoint { 
    # Enter your script to process requests.
}
```

![](../.gitbook/assets/image%20%28134%29.png)

