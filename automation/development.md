---
description: Developing scripts in VS Code
---

# Development

The [Visual Studio Code extension for PowerShell Universal](https://marketplace.visualstudio.com/items?itemName=ironmansoftware.powershell-universal) provides integration for working with automation. We recommend you also install the [PowerShell extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell). 

## Developing Scripts

To add scripts to the Universal platform, you can do it via the admin console or the file system. The Visual Studio Code extension also provides integration for managing the `scripts.ps1` configuration file. 

The Scripts tree view will provide access to each of your scripts, the admin console the `scripts.ps1` file.

![](../.gitbook/assets/image%20%28120%29.png)

To add a new script to the Universal platform, you can create the PS1 file on the file system and then add the script to the `scripts.ps1`. The file name is relative to the repository folder. You can also use fully qualified file paths. 

```PowerShell
New-PSUScript -Name "Script1.ps1" -Path "Script1.ps1" -InformationAction "Continue"
```

To edit a script in VS Code, click the Edit Script button. 

![](../.gitbook/assets/image%20%28119%29.png)

The script will open in the VS Code editor. 

## Running Scripts

You can start scripts by clicking the Run Script button. This will start a Universal Automation job. You'll get notifications of the job's progress in VS Code. 

![](../.gitbook/assets/image%20%28128%29.png)

## Developing Schedules

You can edit schedules for scripts by editing the `schedules.ps1` file. A link to the file is available in the configuration tree view. 

![](../.gitbook/assets/image%20%28131%29.png)

Schedules are defined using `New-PSUSchedule` cmdlet.

```PowerShell
New-PSUSchedule -Cron "0 */4 * * *" -Script "Script1.ps1" -TimeZone "America/Denver"
```

