---
description: Run AI prompts directly in PowerShell Universal.
---

# AI Agents

AI Agents provide the ability to run AI prompts directly in PowerShell Universal. You can select from popular models, provide a key and run the prompt just like you would other jobs. You can also configure local models via OpenAI's API integration.&#x20;

## Configuring an Agent

### Providers and Models

Click Intelligence \ AI Agent and click Create AI Agent. Select the provide type. This can be:

* Anthropic
* OpenAI
* Custom

Enter the name of the model to use. For example:

* `gpt-5.5`
* `claude-sonnet-4.6`
* `qwen3.6-27B`

If you have selected a hosted model, you will need to add your API key so that PowerShell Universal can access the model on your behalf. If you selected a local model, provide the API URL to access the model.&#x20;

### Context

Each agent can have context defined that will be used it each session. After creating your agent, click the Pencil icon to edit the context for the agent. This context is a markdown file and will be passed in when a prompt job is started.&#x20;

### Authorization

Much like other resources, agents can define a set of roles of users that are allowed to call the agent. By selecting roles, you can provide the minimal set of permissions required for someone to call the agent.&#x20;

## Running Prompts

Once an agent is selected, you can run prompts in a couple of different ways: ad hoc, as part of a workflow, using `Invoke-PSUAiAgent`.&#x20;

### Ad Hoc

You can click the run icon next to the AI Agent to run a prompt in the agent. This will initiate an AI Prompt job within the PSU job execution system.&#x20;

### Workflows

You can pull AI Prompts into workflows. This allows data to stream between prompts or from PowerShell scripts. You can instruct your agent to access data from the previous step in the workflow by telling it to inspect the `PSUItem` parameter. This is the pipeline data from the previous job and formatted as CliXml.&#x20;

For example, the below prompt would return a list of 5 processes in JSON format.

{% code overflow="wrap" %}
```
Return the top 5 processes by CPU usage as JSON. A list of all running processes are stored in PSUItem as CliXml.
```
{% endcode %}

This output from the agent will be passed to the next activity in the workflow as either `PSUItem` prompts or `$PSUItem` for PowerShell scripts.

### Invoke-PSUAiAgent

You can also call AI Agents externally or within PSU using the `Invoke-PSUAiAgent` cmdlet within the PowerShell Universal module.

{% code overflow="wrap" %}
```powershell
Invoke-PSUAiAgent -Agent "GPT-5.5" -Prompt "Create a new user in the system. The username should be: adam@devolutions.net"
```
{% endcode %}

## Accessing Tools

Agents can access your AI Tools to perform actions within PowerShell Universal. You will need to configure your scripts as AI Tools in order to bring them into agents. Once configured, you can define which tools are available to an agent. Tools can take action as well as return data back to the agent for additional context.&#x20;

Tools have their own set of roles. An agent will not be able to call a tool if the caller of the agent does not hold the role necessary for this process. For scheduled calls, like when scheduling a workflow, the caller is the system and will have access to all the tools that have been assigned.&#x20;
