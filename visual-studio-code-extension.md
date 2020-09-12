---
description: Learn about the Visual Studio Code extension for Universal.
---

# Visual Studio Code Extension

PowerShell Universal can be managed with the PowerShell Universal Visual Studio Code extension. It allows you to connect to a local Universal instance and manage APIs, dashboards and scripts. 

## Installation

You can download the extension from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ironmansoftware.powershell-universal). You can also download the extension from within the Visual Studio Code extension pane. Search for PowerShell Universal and click Install.  

![](.gitbook/assets/image%20%28117%29.png)

## Configuration

When the extension first installs, it will download the latest version of PowerShell Universal for your platform and store it in `%AppData%\PowerShellUniversal`. It will then start the server, login and generate an app token. The installation directory and app token as stored in settings. 

![](.gitbook/assets/image%20%28114%29.png)

## Features

The PowerShell Universal extension adds a new activity pane panel for PowerShell Universal. It has the following sections. 

### APIs

You can manage APIs with the extension. You will see a list of APIs. You can click the `Open endpoints.ps1` button to view the endpoints file and add new endpoints. Clicking the refresh button will reload any endpoints you add. You can click the `Insert Invoke-RestMethod to Console` to add a call to the endpoint to the PowerShell Integrated Console. 

![](.gitbook/assets/image%20%28113%29.png)

### Dashboards

You can manage dashboards with the extension. You will see a list of dashboards underneath this section. You can open the dashboards.ps1 script, open the a single dashboard's script, restart a dashboard and view dashboards. When you open a dashboard script, the dashboard modules will automatically be loaded so that IntelliSense works in VS Code. 

![](.gitbook/assets/image%20%28118%29.png)

#### Debug Dashboard Process

You can connect the Visual Studio debugger to the dashboard process by right clicking on the dashboard and click Debug Dashboard Process. This requires the PowerShell extension for Visual Studio Code. 

![](.gitbook/assets/image%20%28121%29.png)

After connecting the debugger, you can run commands such as `Get-Runspace` and `Debug-Runspace` to begin debugging aspects of your dashboard. 

#### View Dashboard Logs

You can view dashboard logs by right clicking on the dashboard and clicking View Logs. They will open in a new tab.

![](.gitbook/assets/image%20%28119%29.png)

### Scripts

You can manage scripts with the extension. You will see a list of available scripts underneath this section. You can edit the scripts.ps1, edit an individual script and run scripts. When running scripts, you will receive feedback about the status of the script. Scripts with parameters are not supported in VS Code. You can still run them in PowerShell Universal. 

![](.gitbook/assets/image%20%28115%29.png)

