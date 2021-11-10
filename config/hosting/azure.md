---
description: Learn how to host PowerShell Universal in Azure.
---

# Azure

PowerShell Universal is an ASP.NET Core web application and can be hosted in Windows Azure Web Apps.&#x20;

## Manually Creating a Web App

Within the the Azure Portal, you will need to create a new Web App resource. PowerShell Universal currently requires the .NET 5 runtime stack. You can use either Linux or Windows.

![](<../../.gitbook/assets/image (304).png>)

In this example, we'll use the Azure PowerShell module to deploy the Web App manually.&#x20;

You'll first need to install Azure PowerShell.&#x20;

```
Install-Module Az
```

Once installed, you'll need to connect to your subscription.&#x20;

```
Connect-AzAccount
```

Now, you can download the latest version of PowerShell Universal. In this example, we'll download the latest Linux version.&#x20;

```
$LatestVersion = Invoke-RestMethod https://imsreleases.blob.core.windows.net/universal/production/version.txt
Invoke-WebRequest "https://imsreleases.blob.core.windows.net/universal/production/$LatestVersion/Universal.linux-x64.$LatestVersion.zip" -OutFile .\Universal.zip
```

Now that we have the Az module configured and the Universal ZIP downloaded, we can deploy the Web App.&#x20;

```
$Parameters = @{
    Force = $true
    ResourceGroupName = 'psu-demo'
    Name = 'psudemo'
    ArchivePath = '.\Universal.zip'
}
Publish-AzWebApp @Parameters
```

After publishing the Web App, view your PowerShell Universal instance by navigating to the Web App's URL.

## Updating your Web App

When a new version of PowerShell Universal is released, you will need to update the application files for your Web App. We recommend removing the application directory and redeploying the files. The database and configuration files are not stored in the application directory.&#x20;

You can delete the files for your Web App by using the Kudu command API. Your Kudu credentials use Basic authentication and are the same as your [deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).

To delete all the files in your Web App, issue the following command.&#x20;

```
$Parameters = @{
   Uri = "https://psudemo.scm.azurewebsites.net/api/command"
   Credential = (Get-Credential)
   Body = (@{
      command = "rm -r /home/site/wwwroot"
      dir = "/home/site/wwwroot"
   } | ConvertTo-Json)
}

Invoke-RestMethod @Parameters
```

Once you've delete the application files, you can redeploy them by running the manual creation steps again.
