---
description: Chain together activities with PowerShell Universal workflows.
---

# Workflows

PowerShell Universal workflows let you chain scripts and AI prompts into a single automation flow. Workflows are useful when you need to pass output from one step to the next, branch based on previous results, or add AI-assisted processing between automation steps.

Workflows can be created in the admin console and managed from PowerShell. When a workflow runs, it creates a workflow job that you can monitor from the same job history used for scripts.

## Creating a Workflow

To create a workflow in the admin console, go to Automation / Workflows and click Create Workflow.

Workflows require a name and can optionally define parameters. These parameters are shown when the workflow is started manually and are available to expressions and activities during execution.

## Using the Workflow Designer

The workflow designer provides a visual editor for laying out and configuring your workflow. When you open a workflow, PSU displays the designer for that workflow definition.

### Adding Activities

PowerShell Universal supports script and AI prompt activities in workflows. Under the hood, workflows also use container activities such as flowchart and sequence nodes to define the overall layout.

To add an activity, drag it from the activity pane on the left side of the designer into a drop zone on the canvas.

### Setting Activity Properties

Select an activity to edit its properties in the pane on the right. The available properties depend on the activity type.

For script activities, PSU surfaces the script's PowerShell parameters as activity properties. This makes it possible to bind fixed values or runtime expressions without rewriting the script just for workflow use.

### Using PowerShell Expressions

Some activity properties support PowerShell expressions. Expressions are evaluated at runtime and can reference workflow input values and output from the previous activity.

Use expressions when a property value should be calculated at runtime instead of stored as a fixed literal. For example, you can enable or disable behavior based on a workflow parameter or select values from the previous step's output.

## Workflow Data

Expressions and activities can access workflow state through built-in variables.

### Workflow Object

Use the `$Workflow` variable in PowerShell expressions to access workflow parameter values.

For example, you can set a Boolean property based on the selected environment.

{% code overflow="wrap" %}
```powershell
$Workflow.Environment -eq "Production"
```
{% endcode %}

You can also pass a string workflow parameter directly into an activity property.

{% code overflow="wrap" %}
```powershell
$Workflow.Environment
```
{% endcode %}

Workflow parameters are defined on the workflow itself. Use them for values that should be provided when the workflow starts, such as an environment name, retention period, or approval target.

### PSUItem

The `$PSUItem` variable provides access to the output from the previous activity. The object type depends on what that activity returned.

For example, a script can accept `$PSUItem` as input.

{% code overflow="wrap" %}
```powershell
param($PSUItem)

$PSUItem.MyValue
```
{% endcode %}

You can also reference `PSUItem` in AI prompts.

{% code overflow="wrap" %}
```
PSUItem contains a list of processes. Return the process using the most memory as JSON.
```
{% endcode %}

You can also use `$PSUItem` or `$Output` in PowerShell expressions to change an activity's behavior based on the previous activity's output.

{% code overflow="wrap" %}
```powershell
$PSUItem.ProcessMemory -gt 100
```
{% endcode %}

Use `$PSUItem` when you want to pass structured output from one activity into the next. This is the main way to build multi-step workflows without storing intermediate state elsewhere.

## Example Workflow Pattern

One common pattern is:

1. Run a script to gather data.
2. Pass the output to an AI prompt or another script.
3. Use the result in a final script to take action.

For example:

- A script activity returns a list of processes.
- An AI prompt identifies the process using the most memory.
- A final script receives that result through `$PSUItem` and sends a notification.

This approach keeps each step focused and makes the workflow easier to test and troubleshoot.

## Running Workflows

### On Demand

Workflows can be run on demand by clicking the Play icon in the admin console. If the workflow defines parameters, PSU prompts for them in the run dialog. After the workflow starts, PSU redirects you to the workflow job page.

### Scheduling

Workflows support the same scheduling options as scripts, including CRON, one-time, and continuous schedules. You can create workflow schedules from Automation / Schedules or by assigning a schedule directly to the workflow.

Use schedules when the workflow should run without manual input, such as nightly cleanup, environment validation, or periodic AI-assisted classification.

### Invoke-PSUWorkflow

`Invoke-PSUWorkflow` allows you to execute workflows from PowerShell or from other parts of the PowerShell Universal platform. Like `Invoke-PSUScript`, you can provide parameter values when you invoke the workflow.

## Managing Workflows with PowerShell

You can manage workflows through the Universal module in addition to the admin console.

The core workflow cmdlets are:

- `Get-PSUWorkflow`
- `New-PSUWorkflow`
- `Set-PSUWorkflow`
- `Remove-PSUWorkflow`
- `New-PSUWorkflowParameter`
- `New-PSUWorkflowActivity`
- `Invoke-PSUWorkflow`

### Defining Workflow Parameters

Use `New-PSUWorkflowParameter` to define workflow input metadata such as a default value, whether the parameter is required, and the help text shown to users.

```powershell
$Parameters = @(
	New-PSUWorkflowParameter -Name Environment -DefaultValue Development -Required -HelpText 'Target environment'
)
```

### Defining Activities in PowerShell

Use `New-PSUWorkflowActivity` to create workflow activity definitions.

- Use `-Parameters` for literal values.
- Use `-Expressions` for runtime-evaluated PowerShell expressions.
- For `-Type Script`, PSU can surface dynamic parameters from the target script.

```powershell
$Deploy = New-PSUWorkflowActivity -Type Script `
	-Name Deploy `
	-ScriptFullPath 'C:\ProgramData\UniversalAutomation\Repository\scripts\Deploy.ps1' `
	-FailOnScriptError $true

$Root = New-PSUWorkflowActivity -Type Sequence -Name Deployment -Parameters @{
	Activities = @($Deploy)
}
```

### Creating a Workflow in PowerShell

`New-PSUWorkflow` accepts either a raw definition string or a script block that returns a single workflow activity definition.

```powershell
$Parameters = @(
	New-PSUWorkflowParameter -Name Environment -DefaultValue Development -Required -HelpText 'Target environment'
)

$Deploy = New-PSUWorkflowActivity -Type Script `
	-Name Deploy `
	-ScriptFullPath 'C:\ProgramData\UniversalAutomation\Repository\scripts\Deploy.ps1' `
	-Expressions @{ Environment = '$Workflow.Environment' }

$Root = New-PSUWorkflowActivity -Type Sequence -Name Deployment -Parameters @{
	Activities = @($Deploy)
}

New-PSUWorkflow -Name ApplicationDeployment -Description 'Deploy an application through a workflow' -WorkflowParameters $Parameters -Definition { $Root }
```

## Monitoring Workflow Runs

Workflow runs appear in the job history just like script jobs. Use the job page to inspect:

- current status
- stream output
- pipeline output
- errors

This is the best place to troubleshoot failed workflow steps and verify the data being passed between activities.

## Troubleshooting

- If a property should be calculated at runtime, use an expression instead of a fixed value.
- `$PSUItem` only contains the previous activity's output. The first activity in a workflow will not have prior output.
- Script activity properties are based on the target script metadata. If a script parameter does not appear as expected, verify the script path and parameter name.
- Activity parameter names and expression keys must match valid properties for that activity type.
- If you need recurring execution, attach a schedule rather than manually invoking the workflow.

## Related Topics

- [Jobs](jobs.md)
- [Schedules](schedules.md)
- [Scripts](scripts/)

