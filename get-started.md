---
description: Get started with PowerShell Universal
---

# ⏯️ Get Started

## Install PowerShell Universal

You'll need to install the PowerShell Universal server. [There are a lot of ways to do so,](getting-started/) but you can use the command line below to get started quickly:

{% tabs %}
{% tab title="Windows" %}
You can install PowerShell Universal as a service. Ensure that PowerShell is running as administrator, or the service won't install correctly.

```powershell
Install-Module Universal
Install-PSUServer
```
{% endtab %}

{% tab title="Linux" %}
You can install PowerShell Universal using the following shell script:

```
Install-Module Universal
Install-PSUServer
```
{% endtab %}

{% tab title="Mac OS X" %}
You can install PowerShell Universal using the Universal PowerShell module:

```
Install-Module Universal
Install-PSUServer -AddToPath
Start-PSUServer -Port 5000
```
{% endtab %}

{% tab title="Raspberry PI OS" %}
```
wget https://imsreleases.blob.core.windows.net/universal/production/2.4.0/Universal.linux-arm.2.4.0.zip
unzip Universal.linux-arm.2.3.2.zip -d ./PSU
chmod +x ./PSU/Universal.Server
./PSU/Universal.Server

```
{% endtab %}
{% endtabs %}

## Open PowerShell Universal

By default, PowerShell Universal runs on port 5000 of localhost.

### First Run Wizard

The first run wizard will step you through the basic settings of PowerShell Universal. This includes the default admin username and password, security settings, telemetry settings and license.

<div data-with-frame="true"><figure><img src=".gitbook/assets/image (229).png" alt=""><figcaption><p>Figure shows the final step of the first run with the license key entered</p></figcaption></figure></div>

#### Admin Account

The admin account is used to login to PowerShell Universal. It will display a warning if the password does not match the complexity requirements. You can always change it later.

#### Security Settings

Select from the drop down of security settings. They tweak certain features of PowerShell Universal in different levels of security. If you plan on cloning from a git repository, skip this step or set it to default.

#### Telemetry

PowerShell Universal can [send anonymous telemetry data](platform/telemetry.md) if you opt-in to do so. If you plan to clone from a git repository, skip this setting.

#### License

Add your license file. This is optional and needs to be an account-based license key.

## Create an API

APIs allow you to call PowerShell scripts over HTTP. To create an API, click API \ Endpoints and click Create New Endpoint. Specify a URL.

Next, click details on your new API and enter the following command into the editor:

```
Get-ComputerInfo
```

Save the script and then click the Execute button to test it out.

You can also execute the API via `Invoke-RestMethod`.

```
PS C:\Users\adamr> Invoke-RestMethod http://localhost:5000/hello-world

WindowsBuildLabEx                                       : 22000.1.amd64fre.co_release.210604-1628
WindowsCurrentVersion                                   : 6.3
WindowsEditionId                                        : Professional
WindowsInstallationType                                 : Client
WindowsInstallDateFromRegistry                          : 8/6/2021 4:05:12 PM
WindowsProductId                                        : 00330-52452-93139-AAOEM
WindowsProductName                                      : Windows 10 Pro
WindowsRegisteredOrganization                           :
```

## Create a Script

To create a script, click Automation \ Scripts and then click Create New Script.

Enter the following script into the editor and save:

```powershell
Read-Host "What should I say?"

1..100 | ForEach-Object {
    Write-Progress -PercentComplete $_ -Activity "Processing..."
}

Get-Service
```

Once the script is saved, click Run.

## Create an App

To create a new PowerShell-based user interface (app), you can click User Interfaces \ Apps and then Create New App.

After clicking Ok, click the Details button to edit the PowerShell script. Add the following script to the editor:

```powershell
New-UDApp -Title "Hello, World!" -Content {
    New-UDButton -Text "Click Me" -OnClick {
        Show-UDToast -Message 'Success!!'
    }
}
```

Save the app, click the Restart button and then click the View button. Click the Click Me button.

Learn more about the various features of PowerShell Universal:

* [APIs](api/about.md)
* [Automation](automation/about.md)
* [Apps](apps/building-dashboards.md)
