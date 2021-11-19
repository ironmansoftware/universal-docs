---
description: Information about user sessions.
---

# Sessions

Universal Dashboard maintains sessions for users within each dashboard. There are several locations you can configure user session information. 

## Dashboard Session Setting

Session settings for a dashboard are use the web server session setting by default. You can set the dashboard session timeout for an individual dashboard by using the `-SessionTimeout` on `New-PSUDashboard`. The timeout value is in minutes. 

```text
New-PSUDashboard -Name 'dashboard' -BaseUrl / -Framework UniversalDashboard:Latest -SessionTimeout 30
```

Dashboard sessions are sliding and will not expire while the window is open and active. Some browsers will pause tabs which will cause the session to expire after the time out. 

Restarting a dashboard will cause all sessions to disconnect. 

## Web Server Session Setting

The web server will maintain a session for the user. The session is sliding and will not expire while the window is open and active. Some browsers will pause tabs which will cause the session to expire after the time out.  

The default value for the web server session timeout is 25 minutes. You can change the web server session setting by updating the `appsettings.json` file. 

```text
"SessionTimeout": 25
```

## Dashboard Idle Timeout

In addition to dashboard session timeout, you can also timeout the dashboard when it is idle. Even if the window is open, if the user does not click, type or move the mouse for the idle timeout period, the window will time out. This functionality is disabled by default. 

You can set the idle timeout in minutes by setting the `-IdleTimeout` parameter of `New-PSUDashboard` cmdlet. 

```text
New-PSUDashboard -Name 'dashboard' -BaseUrl / -Framework UniversalDashboard:Latest -IdleTimeout 30
```

## IIS Timeouts

IIS can cause timeouts of sessions in numerous ways. You will need to configure your application pool settings to avoid recycling which will cause all dashboard sessions to be removed. 

Within the advanced settings dialog for the application pool, you can set the recycling settings accordingly. 

![](../../.gitbook/assets/image%20%28281%29.png)

