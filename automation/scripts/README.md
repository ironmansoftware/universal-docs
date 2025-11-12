---
description: PowerShell scripts to execute within PowerShell Universal.
---

# Scripts

You can create PowerShell scripts within PowerShell Universal to execute manually, on a schedule, or when events happen within the platform. They are stored on disk and they persist to a local or remote Git repository.

{% hint style="info" %}
The `scripts.ps1` configuration file stores the Script properties.
{% endhint %}

## Add a New Script

To add a new script, click the New Script button within the Automation / Scripts page. There are various settings you can provide for the script.

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption><p>New Script Dialog</p></figcaption></figure>

## Script Options

### **Name**

This is the name of the script as shown in Universal Automation. This is also the name used to persist the script to disk. The name needs to be unique within the current folder.

### Module and Command

See [Modules and Commands](./#modules-and-commands) below.

### **Description**

This description of the script shows in various places within the UA UI and is returned by the Universal cmdlets.

### **Disable Manual Invocation**

This prevents a script from running manually. This is enforced in the UI as well as the web server and cmdlets.

### **Max Job History**

The max job history defines the amount of jobs stored when running this script. It defaults to 100. Jobs are also cleaned up based on the server-wide job retention duration setting from the Settings / General page.

### **Error Action**

The error action changes how the script reacts when it has an error. By default, terminating and non-terminating errors are ignored and the script always succeeds. You can change this setting to stop to cause scripts to fail immediately when an error is encountered.

If you wish to write errors directly to the error pane without causing changes in how the script is handled (for example in an exception handler), use `Write-PSUError` to output the error record and it appears in the job's error tab.

### **Environment**

This allows you to define the required PowerShell environment for the script. By default, it uses the server-wide default PowerShell environment. PowerShell environments are automatically located the first time the Universal Server starts up or read from the `environments.ps1` file. You can also add Environment on the Settings / Environments page.

### **Timeout**

The number of minutes before the script times out. The default value of 0 means the script will run forever. Once a script reaches its timeout, it is canceled.

### Discard Pipeline

When checked, this disables pipeline output storage. This greatly reduces jobs' CPU and storage overhead, but the script still writes to the information, warning, and error streams.

### **Concurrent Jobs**

Defines the maximum concurrent jobs with which the script can be run. It defaults to 100.

```powershell
New-PSUScript -Name Script.ps1 -Path Script.Ps1 -ConcurrentJobs 1
```

## Running a Script

You can run a script in the UI from the Automation / Scripts page by clicking Run or by clicking View and then Run. In each case, the Run Dialog appears, allowing you to select various settings for the job.

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption><p>Run Script Dialog</p></figcaption></figure>

### Running a Script With Parameters

{% hint style="info" %}
Learn more about parameters [here](parameters.md).
{% endhint %}

PowerShell Universal automatically determines the parameters as defined within your scripts. It takes advantage of static code analysis to determine the type, default values and some validation that is then presented within the UI.

For example, you may have a script with the following parameters:

```powershell
param(
    $Test,
    [DateTime]$Time, 
    [int]$Number,
    [PSCredential]$Credential,
    [System.ConsoleColor]$Color
)
```

The result is a set of input options based on the types of parameters.

<figure><img src="../../.gitbook/assets/image (90).png" alt=""><figcaption><p>Script Parameters Dialog</p></figcaption></figure>

### Running a Script as Another User

{% hint style="info" %}
The integrated [environment](../../config/environments.md) does not support running as alternate credentials.
{% endhint %}

You can run scripts as another user by configuring [secret variables](../../platform/variables.md#creating-a-secret-variable). PowerShell Universal uses the Microsoft Secret Management module to integrate with secret providers. See variables for more information on secrets.

1. Create a new PSCredential secret variable.

Click Platform \ Variables and then click Create Secret. Select the PSCredential variable type. Enter the username and password. Ensure that the Disable Run As Support value is unchecked.

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Create Secret Variable</p></figcaption></figure>

2. Run the Script and select the credential

Navigate back to Automation \ Scripts and click the Run Script button. Select an environment besides the Integrated environment. By default, this will be either PowerShell 7 or Windows PowerShell 5.1.

You will now be prompted with the Run As drop down to select the credential. From there, you can select the credential within the run dialog.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Run as a User</p></figcaption></figure>

### Running a Script on Another Computer

You can use the Computer dropdown to select other machines on which to run a script. The default value is to run on any available computer.

### Running a Script on All Computers

You can run a script on all computers by selecting the All Computers option from the Computer dropdown.

### Running a Script from an App with Output

If you would like to run a script from an app and display the output as it runs, using the following example. It takes advantage of `Invoke-PSUScript` and `Get-PSUJobOutput`.

```powershell
New-UDButton -OnClick {
    $Job = Invoke-PSUScript -Name Script.ps1
    while($Job.Status -eq 'Running' -or $Job.Status -eq 'Queued')
    {
        [array]$Output = Get-PSUJobOutput -Job $Job
        $Job = Get-PSUJob -Id $Job.Id
        $Session:Code = $Output | ForEach-Object { 
            "$_`r`n"
        } | Join-String 
        Sync-UDElement -Id 'code'
        Start-Sleep -Seconds 1
    }
} -Text 'Run Script'

New-UDDynamic -Id 'code' -Content {
    if ($Session:Code)
    {
        New-UDSyntaxHighlighter -Code $Session:Code -Language batch
    }
}
```

### Load Balancing

PowerShell Universal uses a least-busy server loading balancing algorithm. If more than one server is a valid target for a job, PowerShell Universal will select the server with the least number of jobs running on that server.

## Remoting

You can use PowerShell remoting by taking advantage of `Invoke-Command` . PowerShell Universal does not support the use of `Enter-PSSession` or `Import-PSSession`.

## Comment-Based Help

You can use comment-based help to define the description, a synopsis, parameter-based help, and links for your scripts. These will be displayed within the PowerShell Universal UI.

```powershell
<#
.SYNOPSIS 

This is a script for pinging other computers. 

.DESCRIPTION

This script can ping other computers. 

.PARAMETER HostName

The host name or address to ping. 

.LINK
https://www.ironmansoftware.com
#>
param($HostName)

Test-NetConnection $HostName
```

The above yields the following user interface. The synopsis displays as the short description, and a longer description displays in the description section. Links appear under the description.

<figure><img src="../../.gitbook/assets/image (94).png" alt=""><figcaption><p>Additional Script Information</p></figcaption></figure>

## Modules and Commands

Commands and cmdlets found in modules can be used as the target for scripts rather than authoring the script directly.

Let's assume that we have a module called `PSUModule` that contains the following function.

```powershell
function Show-HelloWorld {
    param($Name)
    "Hello, $Name!"
}
```

It's possible to expose this function as a script by using the following syntax in `scripts.ps1`.

```powershell
New-PSUScript -Module 'PSUModule' -Command 'Show-HelloWorld'
```

The function surfaces just like other scripts within the admin console. Parameters, help text and other PSU features work the same as with scripts.

## Statistics

Using a script's job history, PowerShell Universal will provide basic statistics about the execution of the script. These include success rate, average execution time, and breaks downs of environment, user and computer execution.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Script Stats</p></figcaption></figure>

## Start-Job Support

While it's possible to start jobs using Invoke-PSUScript, it may be desirable to start a job using the PowerShell Start-Job cmdlet. Using Start-Job does not register the job with PowerShell Universal and the execution information will not be present in the jobs table.

The Integrated, PowerShell 7 and Windows PowerShell 5.1 environments are not compatible with Start-Job because they are custom PowerShell hosts. In order to use Start-Job, you will need to configure a custom PowerShell environment. Click Settings \ Environments. Next, click Create New Environment. Name the environment, select the Custom environment type and specify pwsh.exe as the executable path.

You will now be able to use this environment to run the Start-Job cmdlet.

## API

* [New-PSUScript](../../cmdlets/New-PSUScript.txt)
* [Remove-PSUScript](../../cmdlets/Remove-PSUScript.txt)
* [Set-PSUScript](../../cmdlets/Set-PSUScript.txt)
* [Get-PSUScript](../../cmdlets/Get-PSUScript.txt)
