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

Below is a list of some modules we have experienced issues with.

* dbatools - Memory usage and leaked database connections
* PSFramework - Memory usage
* VMware PowerCLI - Connection management is scoped to the process
* Az - Connection management is scoped to the process

## Leverage Custom Modules

Building custom modules ensures that you can use the same functionality throughout the PowerShell Universal platform without duplicating code. You can use the same functions in APIs, scripts and dashboards without having to duplicate the logic.&#x20;

Reducing the amount of script an any of these places can help you to better test and isolate issues that are caused by integrating with the platform or by the module itself.&#x20;

Also consider building functions to wrap complex dashboard components. This reduces the overall complexity of the dashboard script and makes it easy to debug and read.&#x20;

## Reduce Unnecessary Job Output

While storing job output is useful for auditing, storing all job output can cause your storage to balloon in size which in turn will slow the performance of your PowerShell Universal system. Some steps you can take to keep job output in check are as follows.&#x20;

#### Discard Pipeline Output

If you aren't going to use pipeline output, you can instruct PowerShell Universal to discard it. This will reduce the amount of data stored as well as increase the performance of your jobs because the system doesn't need to serialize all output to for storage. You will still see your output streams in the job log.&#x20;

#### Take Advantage of Streams&#x20;

Using Debug, Warning and Error streams can help to reduce what is shown in the job by default. Setting the action preference per stream can allow you to disable certain streams for regular operations but enable streams when the job is experience problems.&#x20;

For example, if you use `Write-Debug` throughout your script, you can disable that via the `$DebugActionPreference` variable by setting it to `SilentlyContinue`. If the job were to start to experience problems, you could set it to `Continue` to view the output in the log.&#x20;

#### Utilize Out-Null

`Out-Null` can capture would-be pipeline output and discard it. If you don't want to discard all pipeline output, you can discard some of it by using `Out-Null`. This will improve performance and reduce the size of your job data.&#x20;

## Use Functions in Dashboards

When creating complex sections of a dashboard, it's advised to wrap it in a function to better organize and isolate that complex section. Highly nested dashboards are hard to debug and make it easy to introduce syntax errors that will affect the entire dashboard.&#x20;

We also recommend using modules to store your functions to further reduce the size and complexity of your core dashboard script. Additionally, modules can then be shared across dashboards.&#x20;

