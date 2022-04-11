---
description: PowerShell Universal desktop mode.
---

# Desktop Mode

Desktop mode runs PowerShell Universal as a desktop application. It installs to the current user's application data folders and does not require administrative access to run. It runs as the current user and with a tray icon to access the console and configuration files.&#x20;

## Install Desktop Mode

To install desktop mode, you can [download ](https://ironmansoftware.com/downloads)the desktop mode installer from our website. You will need the [WebView2 runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/) to run desktop mode. This will eventually be included with our installer.

## Differences in Desktop Mode

Desktop mode runs slightly differently than PowerShell Universal as a service.

### Application Context

The desktop application uses WebView2 to display the PowerShell Universal admin console within the application window. The PowerShell Universal server integrates with the desktop application to provide desktop-specific features based on the configuration of PSU.&#x20;

The desktop application provides a tray icon that can be used to exit PowerShell Universal, view the admin UI and open the configuration folder in VS Code.&#x20;

PowerShell Universal will not run when the user is not logged in so scheduled jobs will not execute.&#x20;

### Configuration

Configuration files are stored in `%AppData%\PowerShellUniversal` rather than the ProgramData folder. You can quickly access the configuration folder by using the PowerShell Universal tray icon.&#x20;

### Dashboards

Desktop mode does not support PowerShell Universal Dashboard v2 frameworks. It actually doesn't support anything except the latest framework version. It will not deploy copies of the framework.&#x20;

### Security&#x20;

Desktop mode runs as the current user as a regular desktop application. It starts the PowerShell Universal web server. The server only listens on localhost and enforces Windows authentication. You will not be able to change security settings for the server. You can still use app tokens to allow local applications rights to access the server.&#x20;



