---
description: Information about user sessions.
---

# Sessions

PowerShell Univeral maintains sessions for users within each app. There are several locations you can configure user session information.&#x20;

## App Session Setting

Session settings for an app are using the web server session setting by default. You can set the app session timeout for an individual appby using the `-SessionTimeout` of `New-PSUApp`. The timeout value is in minutes.&#x20;

```powershell
New-PSUApp -Name 'dashboard' -BaseUrl / -SessionTimeout 30
```

App sessions are sliding and will not expire while the window is open and active. Some browsers will pause tabs which will cause the session to expire after the time out.&#x20;

Restarting an app will cause all sessions to disconnect.&#x20;

## Web Server Session Setting

The web server will maintain a session for the user. The session is sliding and will not expire while the window is open and active. Some browsers will pause tabs which will cause the session to expire after the time out. &#x20;

The default value for the web server session timeout is 25 minutes. You can change the web server session setting by updating the `appsettings.json` file.&#x20;

```
"SessionTimeout": 25
```

## App Idle Timeout

In addition to app session timeout, you can also timeout the app when it is idle. Even if the window is open, if the user does not click, type or move the mouse for the idle timeout period, the window will time out. This functionality is disabled by default.&#x20;

You can set the idle timeout in minutes by setting the `-IdleTimeout` parameter of `New-PSUApp` cmdlet.&#x20;

```powershell
New-PSUApp -Name 'dashboard' -BaseUrl / -IdleTimeout 30
```

## IIS Timeouts

IIS can cause timeouts of sessions in numerous ways. You will need to configure your application pool settings to avoid recycling which will cause all app sessions to be removed.&#x20;

Within the advanced settings dialog for the application pool, you can set the recycling settings accordingly.&#x20;

![Figure shows the recommended recycling settings for IIS](<../.gitbook/assets/image (461).png>)
