# Debugging Scripts

Scripts that run within Universal run within background processes or runspaces which may make it hard to debug what is happening within a script. You can use cmdlets like Write-Debug and Write-Verbose to provide more information in logs for dashboards and jobs. 

### Connecting a Debugger to a Script

To debug a script, you can use the Wait-Debugger cmdlet within your script to pause the script until a debugger is attached. You can then use a debugger, like VS Code, to attach to the process and runspace to view variables, step through code and execute debugging commands. 

PowerShell Pro Tools has a [One-Click Attach feature](https://docs.poshtools.com/powershell-pro-tools-documentation/visual-studio-code/one-click-attach) that makes it easier to debug scripts. 

You can also debug scripts using the built in Enter-PSHostProcess, Get-Runspace and Debug-Runspace cmdlets.

