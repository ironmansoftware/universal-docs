---
description: Learn how to best configure PowerShell Universal.
---

# Best Practices

## Favor Non-Integrated Environments

While the integrated environment is fast and easy to use, it runs all of your PowerShell operations within the PowerShell Universal service. Issues with a single script or endpoint can affect the stability of the system.&#x20;

When using non-integrated environments, an external PowerShell process is started. For APIs and Dashboards, that process can be long running but can be restarted without affecting the rest of the system. With jobs and terminals, a new process is started for each instance of the job and terminal. As jobs and terminals are stopped, the process is terminated and any resources consumed by that process are reclaimed by the system.&#x20;

## Isolate Problematic Modules

Complex PowerShell modules can cause problems with PowerShell Universal. Certain modules are not designed to be hosted in a long running process like PowerShell Universal. You will want to use these modules in transient operations like jobs.&#x20;

For example, dbatools may leak database connections when used directly within PowerShell Universal's integrated environment. To avoid this, you can start an external process by running a PowerShell Universal job in a non-integrated environment. The script will run, the process will terminate, and the database connection will be reclaimed automatically.&#x20;
