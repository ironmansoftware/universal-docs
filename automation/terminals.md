---
description: In-browser PowerShell terminals.
---

# Terminals

{% hint style="info" %}
Terminals require a [license](https://ironmansoftware.com/pricing/powershell-universal).
{% endhint %}

Terminals are in-browser PowerShell consoles that you can execute arbitrary commands within. Terminals are configured to target an environment that you select and can optionally us Run As credentials to run as other users. The history of terminals is maintained within the PowerShell Universal database. You can reconnect to disconnected terminals as long as they haven't timed out.

{% hint style="info" %}
Terminal configurations are stored in `terminals.ps1`
{% endhint %}

## Configure A Terminal

You can configure a new terminal by navigating to Automation \ Terminals and clicking Create New Terminal. You'll be able to select the environment and credential to run the terminal as.

<figure><img src="../.gitbook/assets/image (113).png" alt=""><figcaption><p>List of available terminals</p></figcaption></figure>

## Use a Terminal

To use a terminal, click the Open Terminal button for the terminal you wish to launch. Depending on your configuration, this may start a new PowerShell process based on the environment you selected.

Once the terminal has launched, you'll be able to issue commands.

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption><p>Using a terminal</p></figcaption></figure>

### Stop a Terminal

To stop a terminal, you can navigate to the terminal instances tab on the Terminals page. Click the trash can to stop the terminal.

<figure><img src="../.gitbook/assets/image (116).png" alt=""><figcaption><p>Terminal Instances</p></figcaption></figure>

### Reconnect to a Terminal

If you navigate away from PowerShell Universal, the terminal will go idle. You can reconnect to a terminal by clicking the Open Terminal button for the idle terminal instance.

<figure><img src="../.gitbook/assets/image (120).png" alt=""><figcaption><p>Reconnecting to a terminal</p></figcaption></figure>

Terminals will time out automatically after 5 minutes. You can customize the timeout by setting the `-IdleTimeout` parameter of `New-PSUTerminal`.

## History

Terminal history can be enabled per terminal configuration.

<figure><img src="../.gitbook/assets/image (122).png" alt=""><figcaption><p>Enable Command History</p></figcaption></figure>

When terminal history is enabled, you will be able to view the history of all commands that were executed within the terminal. Click the View Command History button for the instance in question.

<figure><img src="../.gitbook/assets/image (123).png" alt=""><figcaption><p>View Command History</p></figcaption></figure>

You will be able to review what the command was that ran, when it was ran, who started the terminal and what the output of the command was.
