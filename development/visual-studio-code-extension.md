---
description: Learn about the Visual Studio Code extension for Universal.
---

# Visual Studio Code Extension

PowerShell Universal can be managed with the PowerShell Universal Visual Studio Code extension. It allows you to connect to a local Universal instance and manage APIs, dashboards and scripts.&#x20;

## Installation

You can download the extension from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ironmansoftware.powershell-universal). You can also download the extension from within the Visual Studio Code extension pane. Search for PowerShell Universal and click Install. &#x20;

![](<../.gitbook/assets/image (278).png>)

## Configuration

The extension will prompt you for the URL and App Token used to connect to your PowerShell Universal instance. Follow the instructions within the extension when it starts up.&#x20;

### Configure From PowerShell Universal

You can configure the extension by navigating to your PowerShell Universal admin console and then logging in. Navigate to Settings \ Configurations and click Edit with VS Code. A new app token will be generated, and the URL will be set automatically.&#x20;

![Configure From the Admin Console](<../.gitbook/assets/image (43).png>)

### Configure Multiple Connections

You can configure multiple connections by using the Connections setting. Click the Add Connection button to open Settings.&#x20;

![Add Connection](<../.gitbook/assets/image (213).png>)

Next, click the Edit settings.json link underneath the Connections setting.&#x20;

![Settings](<../.gitbook/assets/image (263).png>)

The connections array can have zero to many connections. You can provide names for each connection.&#x20;

```json
"powerShellUniversal.connections": [
    {
        "name": "Remote",
        "url": "http://localhost:5000",
        "appToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9uYW1lIjoiYWRtaW4iLCJodHRwOi8vc2NoZW1hcy54bWxzb2FwLm9yZy93cy8yMDA1LzA1L2lkZW50aXR5L2NsYWltcy9oYXNoIjoiOGNiMjAxYzAtZWQxMy00M2YyLThiMjItNmY1ODkxNjRhZWM2Iiwic3ViIjoiUG93ZXJTaGVsbFVuaXZlcnNhbCIsImh0dHA6Ly9zY2hlbWFzLm1pY3Jvc29mdC5jb20vd3MvMjAwOC8wNi9pZGVudGl0eS9jbGFpbXMvcm9sZSI6IkFkbWluaXN0cmF0b3IiLCJuYmYiOjE2NDQxODMxMzIsImV4cCI6MjEwMjA5OTUyMCwiaXNzIjoiSXJvbm1hblNvZnR3YXJlIiwiYXVkIjoiUG93ZXJTaGVsbFVuaXZlcnNhbCJ9.6Y9Bgwaw8GTpRrH3Qp7TCW-UGdPm85E9NClOCyGBVA8"
    }
],
```

Once you have defined a connection, you can connect to that instance by clicking the Connect to Instance button within the Connections tree view.

![Connect to Instance](<../.gitbook/assets/image (436).png>)

## Features

The PowerShell Universal extension adds a new activity pane panel for PowerShell Universal. It has the following sections.&#x20;

### APIs

You can manage APIs with the extension. You will see a list of APIs. You can click the `Open endpoints.ps1` button to view the endpoints file and add new endpoints. Clicking the refresh button will reload any endpoints you add. You can click the `Insert Invoke-RestMethod to Console` to add a call to the endpoint to the PowerShell Integrated Console.&#x20;

![](<../.gitbook/assets/image (392).png>)

### Apps

You can manage apps with the extension. You will see a list of apps underneath this section. You can open the dashboards.ps1 script, open a single app's script, restart an app and view apps.&#x20;

![](<../.gitbook/assets/image (492).png>)

#### View Dashboard Logs

You can view dashboard logs by right clicking on the dashboard and clicking View Logs. They will open in a new tab.

![](<../.gitbook/assets/image (107).png>)

### Scripts

You can manage scripts with the extension. You will see a list of available scripts underneath this section. You can edit the scripts.ps1, edit an individual script and run scripts. When running scripts, you will receive feedback about the status of the script. Scripts with parameters are not supported in VS Code. You can still run them in PowerShell Universal.&#x20;

![](<../.gitbook/assets/image (346).png>)

## Debugging

{% hint style="info" %}
The Administrator role is required for debugging scripts remotely.
{% endhint %}

As of PowerShell Universal v4.2, you can debug scripts remotely with the PowerShell Universal extension. To enable remote debugging, you will need to set the debugger environment in the settings. This is the process that will be started and will load PowerShell Editor Services.&#x20;

```powershell
Set-PSUSetting -DebuggerEnvironment 'pwsh'
```

When connected to your PowerShell Universal instance, you can expand Platform \ Processes and then locate the process you wish to debug. If you use the `Wait-Debugger` cmdlet in your scripts, they will be displayed within the process and runspace drop down. Click the Attach Runspace command to begin debugging your script.&#x20;

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## Sample Browser

The sample browser can be used to insert samples from the PowerShell Universal Sample Repository into your PowerShell Universal instance. Just save the files it updates and your PowerShell Universal system will reflect the changes.&#x20;

{% embed url="https://youtu.be/HkCVe1PUX0Q" %}

## Settings

Settings can be found within the Visual Studio Code Settings dialog. You can open the settings dialog by press `Ctrl+,`

PowerShell Universal settings can be found under Extensions \ PowerShell Universal.&#x20;

### App Token

The App Token is used for communicating with the PowerShell Universal management API. You can create an App Token manually by navigating to Security \ Tokens within the PowerShell Universal admin console.&#x20;

You can also automatically configure an App Token by click Edit with VS Code within Settings \ Configurations.&#x20;

### Check Modules

The extension will check the version of the Universal and UnviersalDashboard PowerShell modules found on the system. If they aren't installed or are not the latest version, new versions will be installed.&#x20;

### Connections

The Connections array allow for defining multiple PowerShell Universal instance connections.

### Samples Directory

This is the directory to store the PowerShell Universal samples.&#x20;

### Sync Samples

Whether to download samples from GitHub so they are available within the samples browser.&#x20;

### Url

The URL of the PowerShell Universal service. This should be the root URL, such as `http://localhost:5000`. This will be set automatically when clicking Edit in VS Code.&#x20;



