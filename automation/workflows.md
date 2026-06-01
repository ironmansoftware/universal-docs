---
description: Chain together activities with PowerShell Universal workflows.
---

# Workflows

PowerShell Universal workflows all you to chain together scripts and AI prompts to pass data from one job to another.&#x20;

## Creating a Workflow

To create a workflow, click Automation \ Workflows and then Create Workflow. Workflows require a name and can optionally accept parameters.&#x20;

## Using the Workflow Designer

The workflow design provides a visual tool for laying out and configuring your workflows. When you open a workflow for editing, it will display the workflow designer.&#x20;

### Adding Activities

PowerShell Universal supports scripts and AI prompts as activities in workflows. On the left hand side of the designer, you will see the activity selection pane where you can drag and drop activities into your workflow. The activity drop zones will appears as you drag the activity over.&#x20;

### Setting Activity Properties

Once an activity has been added to the workflow, you can edit the properties by clicking on the activity. On the right hand side, the property pane will change based on the activity selected. AI Prompts and scripts will have different properties. Scripts will also surface their PowerShell script parameters as properties for the script activity.&#x20;

### Using PowerShell Expressions

You can use PowerShell expressions in some properties within the property pane. These expressions allow you to run PowerShell to during the evaluation and execution of the workflow activities. They have access to both the workflow state and data from the previous activity was that run.&#x20;

## Workflow Data

### Workflow Object

You can use the `$Workflow` variable in PowerShell Expressions to change the behavior of activities based on workflow parameters.&#x20;

For example, you could set a boolean parameter based on a value.

{% code overflow="wrap" %}
```powershell
$Workflow.Environemnt -eq "Production"
```
{% endcode %}

You could also accept a string into a parameter.&#x20;

{% code overflow="wrap" %}
```
$Workflow.Environment
```
{% endcode %}

### PSUItem

The `$PSUItem` variable provides access to the output from the previous activity. The type of the object depends on the return type of the activity.&#x20;

For example, you can accept a `$PSUItem` parameter within your script.&#x20;

{% code overflow="wrap" %}
```powershell
param($PSUItem)

$PSUItem.MyValue
```
{% endcode %}

You can also reference `PSUItem` in your AI prompts.

{% code overflow="wrap" %}
```
PSUItem contains a list of processes. Return the process using the most memory as JSON.
```
{% endcode %}

You can also use `$PSUItem` or `$Output` in PowerShell Expressions to change an activity's behavior based on the previous activity's output.&#x20;

{% code overflow="wrap" %}
```powershell
$PSUItem.ProcessMemory -gt 100
```
{% endcode %}

## Running Workflows

### On Demand

Workflows can be run on demand by click the Play icon in the admin console. If a workflow defines parameters, you can provide them in the run dialog. Once a workflow starts, you will be redirected to the workflow job page.

### Scheduling

Workflows have access to the same scheduling options as scripts. On the Automation \ Schedules page, you can create the same types of schedules, such as CRON and One Time.&#x20;

### Invoke-PSUWorkflow

`Invoke-PSUWorkflow` allows for executing workflows externally or within other parts of the PowerShell Universal platform. Similar to `Invoke-PSUScript` you can define parameter values.

