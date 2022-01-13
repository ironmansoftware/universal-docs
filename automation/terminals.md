---
description: In-browser PowerShell terminals.
---

# Terminals

{% hint style="info" %}
PowerShell Universal 2.6 or later. Requires a [license](https://ironmansoftware.com/pricing/powershell-universal).&#x20;
{% endhint %}

Terminals are in-browser PowerShell consoles that you can execute arbitrary commands within. Terminals are configured to target an environment that you select and can optionally us Run As credentials to run as other users. The history of terminals is maintained within the PowerShell Universal database. You can reconnect to disconnected terminals as long as they haven't timed out.&#x20;

{% hint style="info" %}
Terminal configurations are stored in `terminals.ps1`
{% endhint %}

## Configure A Terminal

You can configure a new terminal by navigating to Automation \ Terminals and clicking Create New Terminal. You'll be able to select the environment and credential to run the terminal as.&#x20;

![Terminals Page](<../.gitbook/assets/image (305) (1) (1).png>)

## Use a Terminal

To use a terminal, click the Open Terminal button for the terminal you wish to launch. Depending on your configuration, this may start a new PowerShell process based on the environment you selected.&#x20;

![Open Terminal](<../.gitbook/assets/image (309) (1).png>)

Once the terminal has launched, you'll be able to issue commands.&#x20;

![Run Commands in a Terminal](<../.gitbook/assets/image (304) (1).png>)

### Stop a Terminal&#x20;

To stop a terminal, you can navigate to the terminal instances tab on the Terminals page. Click the trash can to stop the terminal.&#x20;

![Stop a Terminal](<../.gitbook/assets/image (295).png>)

### Reconnect to a Terminal

If you navigate away from PowerShell Universal, the terminal will go idle. You can reconnect to a terminal by clicking the Open Terminal button for the idle terminal instance.&#x20;

![Reconnect to a Terminal](<../.gitbook/assets/image (306) (1).png>)

Terminals will time out automatically after 5 minutes. You can customize the timeout by setting the `-IdleTimeout` parameter of `New-PSUTerminal`.
