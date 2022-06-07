# Debugging Scripts

Scripts that run within Universal run within background processes or runspaces which may make it hard to debug what is happening within a script. You can use cmdlets like Write-Debug and Write-Verbose to provide more information in logs for dashboards and jobs.

## Integrated Debugger

{% hint style="info" %}
Requires a [license](https://ironmansoftware.com/pricing/powershell-universal). Debugging is not supported in Windows PowerShell.
{% endhint %}

### Enable Debugger

In order to use the debugger, you need to enable it in the environment to wish to use it within. Click Settings \ Environment and select Enable Debugger.&#x20;

### Use the Debugger

PowerShell Universal integrates directly with the PowerShell debugger. You can include `Wait-Debugger` within your scripts to cause them to pause. Once paused, you will be able to access the runspace by navigating to Platform \ Debugging&#x20;

For example, assume you have a dashboard with a `Wait-Debugger` call included.&#x20;

```powershell
New-UDDashboard -Title "Dashboard" -Content {
    Wait-Debugger
    $Data = @(
        @{Dessert = 'Frozen yoghurt'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Ice cream sandwich'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Eclair'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Cupcake'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
        @{Dessert = 'Gingerbread'; Calories = 159; Fat = 6.0; Carbs = 24; Protein = 4.0}
    ) 

    New-UDTable -Data $Data -Paging -PageSize 2 -PaginationLocation 'top'
}
```

You'll notice that loading the page will result in the dashboard hanging. This is because the debugger is paused.&#x20;

![Paused Dashboard](<../.gitbook/assets/image (391).png>)

You can then view the paused scripts in the debugging table.&#x20;

![Breakpoints](<../.gitbook/assets/image (302) (1).png>)

You can then click the Debug button to open a debug terminal.&#x20;

![Debug Button](<../.gitbook/assets/image (305).png>)

Once within the debug terminal, you can execute commands as well as continue, step into, step out of and step over lines in the script.&#x20;

![Debug Terminal](<../.gitbook/assets/image (334).png>)

Executing commands will execute them directly in the PowerShell Universal runspace. You can inspect variables or execute additional commands in the runspace's context.

![Debug Terminal Commands](<../.gitbook/assets/image (298).png>)

## Logging Scripts

Certain aspects of Universal will log their scripts automatically. Other features may require you log yourself.

### APIs

You can use the Live Log view on the Log tab to view logs for the selected API.&#x20;

### Jobs

Jobs log extensively. You will see console and pipeline output. If you set`$DebugPreference` or `$VerbosePreference` , you will also see those streams in the console output. You can add additional log messages using `Write-Debug` or `Write-Verbose` .

### Dashboards

{% hint style="info" %}
See [dashboard Development](broken-reference) for information on how to use VS Code for development.
{% endhint %}

Dashboards log informational, warning and error messages to their log. It's recommended to use logging when starting a dashboard rather than trying to attach a debugger. You can also use the `$DebugPreference` variable to get additional information during your dashboard startup.

```powershell
$DebugPreference = 'Continue'

New-UDDashboard -Title 'Test' -Content {
    Write-Debug "My dashboard is loading. I have am $user with $roles"

    New-UDTypography -Text 'Hello, world'
}
```

### Authentication and Authorization

You can use the Live Log view on the authentication and role pages to see PowerShell stream output.&#x20;

## Debugging Scripts from a PowerShell Console

You can debug any script within Universal (or any PowerShell process, really) using the debugging cmdlets that are available in PowerShell. These cmdlets allow you to connect to local PowerShell processes, like Universal, and step through your scripts right in the terminal.

### Pausing the Script

First, you will need to ensure that the script will wait for you to connect the debugger before continuing. This means that you'll need to include a `Wait-Debugger` command somewhere in your script.

{% hint style="info" %}
Dashboards will only wait 10 seconds during startup so putting a Wait-Debugger in them may not work. You should rely on the use of $DebugPreference and Write-Debug to diagnosis dashboard startup issues.
{% endhint %}

### Executing your script

Now that you have your script setup to pause and wait for the debugger, you will want to execute your script. For jobs, just start the job. For APIs, you will need to make a request to the API via the endpoint you are trying to test. For dashboards, you will want to load the page in your browser. For authentication and authorization, you will want to login.

### Finding your process ID

Once you have your `Wait-Debugger` command in the script that you want to debug, you'll need to start the script and determine the process it is running within.

#### Jobs

Jobs run in their own isolated process within Universal. All you will have to do is start the job and it will start the process and wait on your `Wait-Debugger` command. Once your job has started, you can use the `Get-UAJob` cmdlet to find that job's process ID.

#### APIs

APIs run in a single PowerShell process. It does not start a new process for each API call. You can locate the API process by finding the pwsh or PowerShell process with the command line that includes `StartApi`.

#### Dashboards

Dashboards run in their own isolated PowerShell process. The process ID is listed in the dashboard table within the Admin Console.

#### Authentication and Authorization

Authentication and authorization scripts run within the Universal server. You can find the `Universal.Server.exe` process and attach to that.

**Integrated Environment**

Any feature running within the integrated environment will be running within the `Universal.Server.exe` process. You will need to attach to this process in order to debug them.&#x20;

### Attaching to the Process and Debugging the Runspace

Once you have the process that you want to attach to, you can do so by using `Enter-PSHostProcess` . Simply specify the process ID that you found in the previous step.

```powershell
Enter-PSHostProcess -id 1231
```

{% hint style="info" %}
Enter-PSHostProcess uses named pipes and requires that you have permission to the process that you are accessing. If you are running Universal as a service you may need to run it as your local account to properly connect to the process.
{% endhint %}

Once you have attached to the process, you will now want to find the runspace where your code is running. To do so, you can use the `Get-Runspace` cmdlet. This will return a list of runspaces currently active in your process. Look for the runspace marked `InBreakpoint`. This is the runspace waiting on the `Wait-Debugger` command.

Now that you found your runspace, use `Debug-Runspace` to attached to the runspace. You will now have the opportunity to issue debugging commands against that runspace. You can view the status of variables, issue commands and even step through the script.

For a full list of debugging commands, you can see the [Microsoft documentation here](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about\_debuggers?view=powershell-7#starting-and-stopping-the-debugger).

### Example of Connecting to API Process

The following is an example of how to connect to an API process.&#x20;

```powershell
$Process = Get-Process pwsh | Where-Object { $_.CommandLine.Contains('StartApi') }
Enter-PSHostProcess -Id $Process.Id
Get-Runspace
Debug-Runspace -Id 2
```

## Debugging with Visual Studio Code

To debug a script, you can use the Wait-Debugger cmdlet within your script to pause the script until a debugger is attached. You can then use a debugger, like VS Code, to attach to the process and runspace to view variables, step through code and execute debugging commands.

You can also debug scripts using the built in `Enter-PSHostProcess`, `Get-Runspace` and `Debug-Runspace` cmdlets.
