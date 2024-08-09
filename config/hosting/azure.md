---
description: Learn how to host PowerShell Universal in Azure.
---

# Azure

PowerShell Universal is an ASP.NET Core web application and can be hosted in Windows Azure Web Apps.

## Container Web App

Container web apps allow for using Docker images as web apps in Azure. Within the Azure portal, you can create a Docker Container web app by using the App Services \ Create Web App wizard.

Once you have selected a resource group, assigned a name and selected a compute plan, you will be able to create the web app.

![Container Web App](<../../.gitbook/assets/image (424).png>)

Next, you'll need to deploy the image to your web app. To do so, select the Deployment Center and configure the image to pull. You can either pull a static tagged version (like 2.7.3) or pull the latest and your web app will automatically stay up to date with new PowerShell Universal releases. Use the tag with the `azure` suffix. It is pre-configured to run in Azure.&#x20;

{% hint style="info" %}
For production environments, we suggest setting a tagged version to avoid unintentional updates to your container when it restarts. By default, Azure will automatically update containers when a tag, such as latest, is updated. This will allow you to control updates to your PowerShell Universal version.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption><p>Docker Configuration</p></figcaption></figure>

### Local Persistence

By default, the container will write to the `/home` directory.&#x20;

You will need to ensure that the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` environment variable is set to true. This configures the container to make the `/home` folder persistent and this is where the configuration data for PowerShell Universal is stored.&#x20;

### Git and SQL

If you choose to use git integration in PowerShell Universal, we recommend setting up a SQL server and database for storage. Git will be used to synchronize configuration files when the container is started. SQL will store the git configuration settings alongside resources like jobs, app tokens and identities.

You'll need an Azure SQL database to get started. Once you create the resource, you will need to copy the connection string from the database to provide to PowerShell Universal.

<figure><img src="../../.gitbook/assets/image (385).png" alt=""><figcaption></figcaption></figure>

Ensure that you have allowed Azure services to access the database.

<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>

To enable SQL support, you should set the plugins within PowerShell Universal to use the SQL plugin in the Application Configuration for your web app.

Create a `Plugins__0` setting with the value `SQL`. Next, set the `Data__ConnectionString` value to your SQL server database.

<figure><img src="../../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

Once you have SQL configured, you can start your container. The database schema will be created as the container starts. Next, you'll need to configure git within PowerShell Universal by clicking Settings \ Git. Enter your remote, branch, username, password or personal access token, and synchronization mode. Push-only is not recommended in this configuration because container state is lost between restarts. Ensure that the initialization mode is set to Clone.

{% hint style="info" %}
Git settings are stored in your SQL database and will be retrieved each time the container is started.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

### Forwarded Headers

Containers are typically hosted behind a reverse proxy and will not be aware of the actual external URL without additional configuration. In order to ensure that systems that require the external URL, like OpenID Connect, receive the proper information, you will need to set the `ASPNETCORE_FORWARDEDHEADERS_ENABLED` environment variable to `true`.

![](<../../.gitbook/assets/image (390).png>)

For more information, you can read this blog post from the [Microsoft](https://devblogs.microsoft.com/dotnet/forwarded-headers-middleware-updates-in-net-core-3-0-preview-6/).

## Standard Web App

### Manually Creating a Web App

Within the Azure Portal, you will need to create a new Web App resource. PowerShell Universal currently requires the .NET 6 runtime stack. You can use either Linux or Windows.

{% hint style="info" %}
If you choose a Windows hosting plan rather than a Linux hosting plan in Azure when configuring your WebApp then you need to choose a Basic Plan (B1) or higher to be able to use 64-bit apps. You also have to go to Settings > Configuration > General setting > Platform and select 64-bit before you run the `Publish-AzWebApp` command, or it will fail to install.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (325).png" alt=""><figcaption></figcaption></figure>

**Startup Command (Linux Only)**

When hosting in a Linux environment, you will need to set the startup command under Settings \ Configuration \ General Settings \ Startup Command to the following.

```
dotnet Universal.Server.dll
```

In the below example, we'll use the Azure PowerShell module to deploy the Web App manually.

You'll first need to install Azure PowerShell.

```powershell
Install-Module Az
```

Once installed, you'll need to connect to your subscription.

```powershell
Connect-AzAccount
```

### Deploy Windows Files

If you are using Windows, you will need to download the Windows ZIP file. This will download the latest version of PowerShell Universal.

```powershell
$LatestVersion = Invoke-RestMethod https://imsreleases.blob.core.windows.net/universal/production/v3-version.txt
Invoke-WebRequest "https://imsreleases.blob.core.windows.net/universal/production/$LatestVersion/Universal.win7-x64.$LatestVersion.zip" -OutFile .\Universal.zip
```

### Deploy Linux Files

If you are using Linux, you will need to download the Linux ZIP file. This will download the latest version fo PowerShell Universal.

```powershell
$LatestVersion = Invoke-RestMethod https://imsreleases.blob.core.windows.net/universal/production/v3-version.txt
Invoke-WebRequest "https://imsreleases.blob.core.windows.net/universal/production/$LatestVersion/Universal.linux-x64.$LatestVersion.zip" -OutFile .\Universal.zip
```

Now that we have the Az module configured and the Universal ZIP downloaded, we can deploy the Web App.

```powershell
$Parameters = @{
    Force = $true
    ResourceGroupName = 'psudemo2_group'
    Name = 'psudemo2'
    ArchivePath = '.\Universal.zip'
}
Publish-AzWebApp @Parameters
```

{% hint style="info" %}
You can check in Azure under Deployment Center > Logs for Status Success (Active) to ensure files deployed / installed successfully.
{% endhint %}

### Setting Adjustments Required

These settings can be set within the Configuration tab within the Application settings.

<figure><img src="../../.gitbook/assets/image (304).png" alt=""><figcaption></figcaption></figure>

#### JWT Signing Key

The default JWT signing key is not of a sufficient length and will need to be updated. This can be done in `appsettings.json` or by using environment variables.

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

#### API URL

Azure Web Apps use a reverse proxy and PowerShell Universal does not detect the external URL appropriately. When running jobs, Universal uses the Management API to automatically look up job, script and schedule information. This means that this will fail if it cannot correctly address the external API URL.

The API URL should be the external HTTP address of your Web App. You can update this in `appsettings.json` or by using an environment variable.

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

#### NodeName

You can set the name of the PowerShell Universal instance by specifying the NodeName. This will ensure that restarts will not affect the PowerShell Universal database. This is not required for LiteDB installations.

```
$Env:NodeName = "psuazure"
```

#### PORT and WEBSITES\_PORT (Linux Only)

To override the default port in a Linux web app, you need to set the PORT and WEBSITES\_PORT setting to 5000.

After publishing the Web App, view your PowerShell Universal instance by navigating to the Web App's URL.

#### Persistent Storage

The default `appsettings.json` file will store the database and configuration files in a non-persistent location. You can add environment variables to move them to persistent storage within your web app.

**Data\_\_ConnectionString**

The `Data__ConnectionString` environment variable sets the location of the database. You will have to ensure that you enable a "shared" connection for LiteDB to function properly in Azure. Set the value to the following.

```
filename=D:\home\Data\PowerShellUniversal\database.db;Connection=shared
```

**Data\_\_RepositoryPath**

The `Data__RepositoryPath` environment variable sets the location of the configuration files for Universal. Set the value to the following.

```
D:\home\Data\PowerShellUniversal\Repository
```

### Updating your Web App

When a new version of PowerShell Universal is released, you will need to update the application files for your Web App. We recommend removing the application directory and redeploying the files. The database and configuration files are not stored in the application directory.

You can delete the files for your Web App by using the Kudu command API. Your Kudu credentials use Basic authentication and are the same as your [deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).

To delete all the files in your Web App, issue the following command.

```powershell
$Parameters = @{
   Uri = "https://psudemo2.scm.azurewebsites.net/api/command"
   Credential = (Get-Credential)
   Body = (@{
      command = "rd /s /q D:\home\site\wwwroot"
      dir = "D:\home\site\wwwroot"
   } | ConvertTo-Json)
}

Invoke-RestMethod @Parameters
```

Once you've delete the application files, you can redeploy them by running the manual creation steps again.

## Application Gateway

You can configure PowerShell Universal to run behind an Application Gateway within Azure. This is helpful for providing load balancing and high availability to multiple PowerShell Universal instances.

First, configure a backend pool that targets one or more Azure Web Apps running PowerShell Universal.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>Backend Pool</p></figcaption></figure>

For the backend settings, you will want to ensure you are using HTTPS with a well known CA certificate. Cookie-based affinity is required to ensure that sessions are sticky to a individual node.

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>Backend Pool Settings</p></figcaption></figure>

In order to allow Azure to serve the proper web app, you will need to ensure that the Override with new host name setting is configured. Use the host name for the backend target.

<figure><img src="../../.gitbook/assets/image (2) (2).png" alt=""><figcaption><p>Backend Settings Host Name</p></figcaption></figure>

Ensure that the backend pool rule is configured as the target and not redirection.

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption><p>Application Gateway Rule</p></figcaption></figure>

Configure a header rewrite rule to pass along the public facing host name as the `X-Forwarded-Host` header. PowerShell Universal will use this to internally construct URLs.

<figure><img src="../../.gitbook/assets/image (8) (2).png" alt=""><figcaption><p>Rewrite Rule</p></figcaption></figure>

The above rewrite rule is a requirement of OpenID Connect and SAML2 authentication methods.

Finally, you can configure your Application Gateway public IP using a DNS provide to a custom host name. Create an A record in your DNS management.

<figure><img src="../../.gitbook/assets/image (10) (2).png" alt=""><figcaption><p>DNS Record</p></figcaption></figure>
