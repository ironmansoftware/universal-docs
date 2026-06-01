---
description: Licensing options for PowerShell Universal
---

# 🔑 Licensing

PowerShell Universal is licensed per server. We provide licenses for individuals and organizations.

You can purchase a license on [our website](https://ironmansoftware.com/pricing/powershell-universal).

## What's a server?

A server is a single running instance of PowerShell Universal.

### What if I have multiple containers?

The license applies to each container instance and not the container host. For example, if you have 10 container instances running, you will need 10 licenses.

### What if I have multiple sites on a single IIS server?

Each website running PowerShell Universal will need a license and not a single license for the entire IIS server.

## Install a License

To install a license, click Settings \ License. Click the Add License button to upload your license file. You can also install licenses using the `Set-PSULicense` cmdlet. Offline licenses do not require an internet connection but will need to be reinstalled when the subscription expires, in you wish to update the version of PowerShell Universal. Online licenses require an internet connection and access to `https://ironmansoftware.com` in order to verify subscription status.

You can use the `PSULICENSE` environment variable to set a license. The value of this environment variable needs to be the contents of the license file.

Proxy configuration can be done by clicking Settings \ General and configuring the proxy URI and, optionally, credentials. You can also configure proxy settings with the `Set-PSUSetting` cmdlet.

### Offline Licenses

Offline license files are required for environments that do not have internet access. You will need to install a new license file when you plan to upgrade to a version past the expiration date of the license.

### Online Licenses

Online licenses work the same as offline but check the subscription status on ironmansoftware.com. The license is tied to a specific subscription and may require a change after renewal. We recommend account-based licensing over online licenses.

## Developer License

You can obtain a free developer license by logging in with a [Devolutions Account](https://docs.devolutions.net/portal/profile/create-devolutions-account/). Using a developer license allows for use in non-production workloads. You can use this license for developing or testing PowerShell Universal.&#x20;

During the first run wizard, you will be presented with the option to login with a Devolutions Account. After doing so, you will be redirected back to PowerShell Universal with a license installed.

<figure><img src=".gitbook/assets/image (328).png" alt=""><figcaption></figcaption></figure>

### Static Login Port

PowerShell Universal, by default, selects a random localhost port in the range `60370` to `61370` for Devolutions login attempts. This is due to restrictions of the authentication provider. If you would like a static localhost port for local or on-host hosted scenarios, you can use the `PSULoginPort` setting or environment variable.

`PSULoginPort` makes the localhost callback port static. It does not change the callback host from `127.0.0.1`. Exposing or forwarding the port may be necessary in some hosted environments, but exposing the port alone does not make Developer License onboarding work for remote browsers through Docker, IIS, or reverse proxy hosting.

{% code overflow="wrap" %}
```json
{
    "PSULoginPort": 60370
}
```
{% endcode %}

### Docker

If you want to use Docker as a mechanism for hosting your development instance of PowerShell Universal, you will need to open a port for the login port. This includes specifying the static login port as well as mapping it out of the Docker instance.&#x20;

{% code overflow="wrap" %}
```
docker run --rm -it `
  -e PSULoginPort=60370 `
  -p 5000:5000 `
  -p 60370:60370 `
  devolutions/powershell-universal
```
{% endcode %}

#### IIS

If you want to use IIS as mechanism for hosting your development instance of PowerShell Universal, you will need to set the static login port as part of your `web.config` file.

{% code overflow="wrap" %}
```xml
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="Universal.Server.exe" arguments="--appsettings .\appsettings.json" forwardWindowsAuthToken="false" stdoutLogEnabled="true" stdoutLogFile=".\logs\log" hostingModel="OutOfProcess">
      <environmentVariables>
        <environmentVariable name="PSULoginPort" value="60370" />
    </environmentVariables>
    </aspNetCore>
  </system.webServer>

</configuration>
```
{% endcode %}

After doing so, you will need to add a new binding for the login port.

<figure><img src=".gitbook/assets/image (329).png" alt=""><figcaption></figcaption></figure>

## Licensed Features

The following features of PowerShell Universal require a license.

* Debugging Tools
* Enterprise Authentication
  * OpenID Connect
  * SAML2
  * WS-Federation
  * Windows Authentication
  * Custom Authentication Scripts
  * Client Certificate
  * App Tokens
* Enterprise Authorization
  * Permissions
  * Custom Authorization Scripts
* Platform
  * Git Support
  * Module Management
  * Non-Database Credential Vaults
  * SQL Support
  * PostgreSQL Support
  * Published Folders
  * Cache Management
  * Computer Groups
  * Translations
* Settings
  * Branding
  * Tags
* APIs
  * Event Hubs
  * OpenAPI Documentation
* Automation
  * Triggers
  * Terminals
  * Tests
  * Workflows
* Intelligence
* Apps
  * App Page Editor
  * App Function Editor
