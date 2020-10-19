# Jobs

Jobs are the result of running a script. Jobs are retained based on the script and server level settings.  

## Viewing Jobs 

Jobs can be viewed by clicking the Automation / Jobs page. Click the View button to navigate to the job. Jobs in progress can also bee cancelled. 

![](../.gitbook/assets/image%20%2819%29.png)

### View Job Output

Standard job output is shown on the Output Tab of the job page. This should contain text from various PowerShell streams. 

![](../.gitbook/assets/image%20%2813%29.png)

### View Job Pipeline Output

Pipeline output for jobs are also stored within UA. Any object that is written to the pipeline is stored as CliXml and available for view within the Pipeline Output tab. 

You can expand the tree view to see the objects and properties from the pipeline. 

![](../.gitbook/assets/image%20%2822%29.png)

### Viewing Errors

Any errors written to the error stream will be available on the Error tab within the job page. 

![](../.gitbook/assets/image%20%2825%29.png)

## Feedback 

Some jobs will require feedback. Any script that contains a Read-Host call will wait until there is user interaction with that job. The job will be in a Waiting for Feedback state and you can respond to that feedback by click the Response to Feedback button on the job page. 

![](../.gitbook/assets/image%20%2817%29.png)

## Parameters

Jobs support automatically generating forms with parameters based on your script's `param` block. The type of control will change based on the type you define in the block. Parameters that are mandatory will also be required by the UI. 

### Basic Parameters

Parameters can be simply defined without any type of parameter attribute and they will show up as text boxes in the UI. 

```text
param($Test)

$Test
```

![](../.gitbook/assets/image%20%2887%29.png)

### Type Parameters

UA supports various types of parameters. You can use String, Int, DateTime, Boolean, Switch and Enum types. 

```text
param(
    [String]$Textbox,
    [Int]$NumberPicker,
    [DateTime]$DateTime,
    [Bool]$Switch,
    [Switch]$Switch2,
    [System.DayOfWeek]$Select
)

$Textbox
$NumberPicker
$DateTime
$Switch
$Switch2
$Select
```

![](../.gitbook/assets/image%20%2888%29.png)

### Required Parameters

You can use the Parameter attribute to define required parameters. 

```text
param(
    [Parameter(Mandatory)]
    $RequiredParameter
)

$RequiredParameter
```

![](../.gitbook/assets/image%20%2886%29.png)

## Invoking Jobs from the Command Line

You can use `Invoke-UAJob` to invoke jobs from the command line. You will need a valid [App Token](../config/security/#app-tokens) to do so. Parameters are defined using dynamic parameters on the `Invoke-UAJob` cmdlet. 

```text
Invoke-UAJob -Script 'Script1.ps1' -RequiredParameter 'Hello'
```

### Call Scripts from Scripts

You can also call UA scripts from UA scripts. When running a job in UA, you don't need to define an app token or the computer name manually. These will be defined for you. You can just call `Invoke-UAScript` within your script to start another script. Both jobs will be shown in the UI. If you want to wait for the script to finish, use `Wait-UAJob`. 

## Return Pipeline Data

You can use the `Get-PSUJobPipelineOutput` cmdlet to return the pipeline output that was produced by a job. This pipeline output will be deserialized objects that were written to the pipeline during the job. You can access this data from where you have access to the PowerShell Universal Management API. 

```text
Get-PSUJobPipelineOutput -JobId 10
```



