---
description: Heatlh checks to run against the PowerShell Universal platform.
---

# Health Checks

Heatlh checks are built in verifications of the PowerShell Universal platform. They will alert you if something is misconfigured or wrong with the PSU instance.

### Built in Health Checks

#### Conflicting Module

This health check looks for conflicting versions of the PowerShell Universal module. We recommend only having the Universal module that matches the version of the server installed on the server.

#### CPU Usage

Checks that the CPU usage of the PowerShell Universal server is less than 80%. This health check is only supported on Windows. The service account running the PowerShell Universal service will need to be part of the Performance Monitor Users group for this health check to function properly.

#### Disk Space

This health check verifies the free space on the disks of the server. It will alert if they are below 20%.

#### Forwarded Token

This health check verifies that the `forwardWindowsAuthToken` setting is present in the `web.config` file when hosting IIS and Windows authentication is enabled. Without this setting present, Windows authentication will not work.

#### IIS WebSocket

This health check verifies that the IIS server has the IIS WebSocket feature enabled. This is required for PowerShell Universal. For this health check to function properly, the user will need access to the `ROOT\CIMv2` namespace for the local WMI provider.

To configure this, you will need to open `wmimgmt.msc`, right click on the WMI Control (Local) node and then click properties. Navigate to the Security tab, select ROOT\CIMv2 and press the Security button to view the access controls for this namespace.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption><p>WMI Security</p></figcaption></figure>

#### Memory Usage

Checks that the memory usage on the server is below 80%

#### PSScriptAnalyzer

Checks that the PSScriptAnalyzer module is installed. PowerShell Universal uses features of this module but does not include it. You can install the module from the PowerShell Gallery.

```powershell
Install-Module PSScriptAnalyzer -Force
```
