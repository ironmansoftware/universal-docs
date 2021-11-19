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

```powershell
Install-Module Az
```

Once installed, you'll need to connect to your subscription.&#x20;

```powershell
Connect-AzAccount
```

### Linux

{% hint style="danger" %}
There is a Known Issue with deploying PowerShell 2.5.x to Linux Web Apps.&#x20;
{% endhint %}

Now, you can download the latest version of PowerShell Universal. In this example, we'll download the latest Linux version.&#x20;

```powershell
$LatestVersion = Invoke-RestMethod https://imsreleases.blob.core.windows.net/universal/production/version.txt
Invoke-WebRequest "https://imsreleases.blob.core.windows.net/universal/production/$LatestVersion/Universal.linux-x64.$LatestVersion.zip" -OutFile .\Universal.zip
```

Now that we have the Az module configured and the Universal ZIP downloaded, we can deploy the Web App.&#x20;

```powershell
$Parameters = @{
    Force = $true
    ResourceGroupName = 'psu-demo'
    Name = 'psudemo'
    ArchivePath = '.\Universal.zip'
}
Publish-AzWebApp @Parameters
```

After publishing the Web App, view your PowerShell Universal instance by navigating to the Web App's URL.

### Windows

Now, you can download the latest version of PowerShell Universal. In this example, we'll download the latest Windows version.&#x20;

```powershell
$LatestVersion = Invoke-RestMethod https://imsreleases.blob.core.windows.net/universal/production/version.txt
Invoke-WebRequest "https://imsreleases.blob.core.windows.net/universal/production/$LatestVersion/Universal.win7-x64.$LatestVersion.zip" -OutFile .\Universal.zip
```

Now that we have the Az module configured and the Universal ZIP downloaded, we can deploy the Web App.&#x20;

```powershell
$Parameters = @{
    Force = $true
    ResourceGroupName = 'psu-demo'
    Name = 'psudemo'
    ArchivePath = '.\Universal.zip'
}
Publish-AzWebApp @Parameters
```

After publishing the Web App, view your PowerShell Universal instance by navigating to the Web App's URL.

### Persistent Storage

The default `appsettings.json` file will store the database and configuration files in a non-persistent location. You can add environment variables to move them to persistent storage within your web app. Note the `Data__ConnectionString` and `Data__RepositoryPath` environment variables.&#x20;

![](<../../.gitbook/assets/image (309).png>)

## Updating your Web App

When a new version of PowerShell Universal is released, you will need to update the application files for your Web App. We recommend removing the application directory and redeploying the files. The database and configuration files are not stored in the application directory.&#x20;

You can delete the files for your Web App by using the Kudu command API. Your Kudu credentials use Basic authentication and are the same as your [deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).

### Linux

To delete all the files in your Web App, issue the following command.&#x20;

```powershell
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

### Windows

To delete all the files in your Web App, issue the following command.&#x20;

```powershell
$Parameters = @{
   Uri = "https://psudemo.scm.azurewebsites.net/api/command"
   Credential = (Get-Credential)
   Body = (@{
      command = "rd /s /q D:\home\site\wwwroot"
      dir = "D:\home\site\wwwroot"
   } | ConvertTo-Json)
}

Invoke-RestMethod @Parameters
```

Once you've delete the application files, you can redeploy them by running the manual creation steps again.

## Setting Adjustments Required

### JWT Signing Key

The default JWT signing key is not of a sufficient length and will need to be updated. This can be done in `appsettings.json` or by using environment variables.&#x20;

#### appsettings.json

```
  "Jwt": {
    "SigningKey": "xXyt9UpJKB4Pb*4$hprd!JJoyOcK4ZOV**O7Hug9&@gYHc$",
    "Issuer": "IronmanSoftware",
    "Audience": "PowerShellUniversal"
  },
```

#### Environment Variable

```
$Env:Jwt__SigningKey = 'xXyt9UpJKB4Pb*4$hprd!JJoyOcK4ZOV**O7Hug9&@gYHc$'
```

### API URL

Azure Web Apps use a reverse proxy and PowerShell Universal does not detect the external URL appropriately. When running jobs, Universal uses the Management API to automatically look up job, script and schedule information. This means that this will fail if it cannot correctly address the external API URL.&#x20;

The API URL should be the external HTTP address of your Web App. You can update this in `appsettings.json` or by using an environment variable.&#x20;

#### appsettings.json

```
"Api": {
 "Url": "https://psudemo.azurewebsites.net"
 },
```

#### Environment Variable

```
$Env:Api__Url = "https://psudemo.azurewebsites.net"
```
