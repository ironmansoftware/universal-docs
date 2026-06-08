---
description: Run AI prompts directly in PowerShell Universal.
---

# AI Agents

AI Agents let you run prompt jobs directly in PowerShell Universal. An agent combines a model, provider settings, instructions, authorization, and optional AI Tools so users can run repeatable prompts inside the PSU job system.

You can run agents from the UI, workflows, the Management API, or the PowerShell Universal module.

## Create an AI Agent

### Providers and Models

Navigate to Intelligence / AI Agents and click Create AI Agent.

Select a provider:

* Anthropic
* OpenAI
* Custom

Then enter the model name. For example:

* `gpt-5.5`
* `claude-sonnet-4.6`
* `qwen3.6-27B`

For hosted models, provide an API key variable so PSU can authenticate on your behalf. For `Custom`, provide an absolute OpenAI-compatible endpoint URL. This is useful for local or self-hosted models.

Typical custom endpoints include local gateways such as vLLM or Ollama-compatible APIs.

### Context

Each agent can include instructions that are used for every prompt. After creating the agent, click the pencil icon to edit its markdown instructions file.

Use this file for stable guidance such as:

* tone and writing style
* expected output format
* operational rules
* references to available tool names

Keep the instructions focused. Put request-specific data in the prompt itself rather than baking it into the agent.

### Tools

Agents can call [AI Tools](ai-tools.md) during execution.

In the AI Tools field, assign one or more tool names or wildcard patterns such as:

* `Get Running Processes`
* `ticket_*`
* `weather*`
* `*`

Leave the field empty to disable tool access for that agent.

### Authorization

Like other PSU resources, agents can define roles that are allowed to execute them. The caller must be authorized for both the agent and any tool the agent attempts to use.

## Running Prompts

You can run prompts ad hoc, in workflows, through the Management API, or with PowerShell cmdlets.

### Ad Hoc

Click the run icon next to an agent to start a prompt job. The prompt runs as a normal PSU job, so you can inspect job history and output from the Jobs page.

### Workflows

You can add AI Prompt steps to workflows. Data from the previous step is available to the agent in the `PSUItem` parameter as PowerShell CliXml.

For example, this prompt asks the agent to inspect workflow input and return JSON:

{% code overflow="wrap" %}
```
Return the top 5 processes by CPU usage as JSON.
The list of all processes is available in PSUItem as CliXml.
```
{% endcode %}

The output is then passed to the next workflow activity as `PSUItem` for another prompt step or `$PSUItem` for a PowerShell step.

### Invoke-PSUAiAgent

Use the PowerShell Universal module to create, review, update, and invoke agents.

Common cmdlets include:

* `Get-PSUAiAgent`
* `New-PSUAiAgent`
* `Set-PSUAiAgent`
* `Remove-PSUAiAgent`
* `Invoke-PSUAiAgent`

Create an agent:

{% code overflow="wrap" %}
```powershell
$apiKey = Get-PSUVariable -Name 'OpenAIKey'

New-PSUAiAgent -Name 'SupportAgent' `
	-Description 'Summarizes incidents and drafts operator-facing responses.' `
	-Provider OpenAI `
	-Model 'gpt-5.5' `
	-ApiKey $apiKey `
	-Tool @('ticket_*', 'Get Running Processes') `
	-Role @('HelpDesk', 'Operator')
```
{% endcode %}

Invoke an agent and wait for the final response:

{% code overflow="wrap" %}
```powershell
Invoke-PSUAiAgent -AiAgent 'SupportAgent' `
	-Prompt 'Summarize the last deployment and call out any failures.' `
	-Wait
```
{% endcode %}

Pass additional parameters to the prompt job:

{% code overflow="wrap" %}
```powershell
Invoke-PSUAiAgent -AiAgent 'SupportAgent' `
	-Prompt 'Draft a status update for the incident.' `
	-Parameters @{
		IncidentId = 42
		Customer   = 'Contoso'
		Severity   = 'High'
	} `
	-Wait
```
{% endcode %}

These additional parameters are serialized as CliXml and appended to the prompt context for the agent.

### Management API

You can also run an agent through the Management API at `/api/v1/aiagent/run`.

{% code overflow="wrap" %}
```powershell
Invoke-RestMethod -Method Post `
	-Uri 'http://localhost:5000/api/v1/aiagent/run' `
	-Headers @{ Authorization = 'Bearer <app-token>' } `
	-Body (@{
		agentName = 'SupportAgent'
		prompt    = 'Summarize the deployment status for today.'
	} | ConvertTo-Json) `
	-ContentType 'application/json'
```
{% endcode %}

The API returns the created job ID or run ID, which you can use to read job output.

## Accessing Tools

Agents can use AI Tools to query PSU data or take action by running approved PowerShell scripts.

Tool access is evaluated at runtime. Even if an agent is allowed to run, a tool call will fail if the caller does not meet the tool's authentication or role requirements.

For scheduled workflow executions, the caller is the PSU system account, so scheduled runs can access any assigned tools that the system is permitted to use.
