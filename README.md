---
description: >-
  A single pane of glass for managing and delegating access to your automation
  environment.
---

# About

<figure><img src=".gitbook/assets/image (354).png" alt=""><figcaption><p>PowerShell Universal Admin Console</p></figcaption></figure>



{% hint style="info" %}
This documentation is for PowerShell Universal v5 beta.&#x20;
{% endhint %}

A single pane of glass for managing and delegating access to your automation environment.

Universal provides an Administrator console, management REST API, PowerShell cmdlets and an idempotent configuration system using PowerShell scripts.

## **APIs**

Expose scripts as RESTful HTTP APIs for integration from any platform.

<figure><img src=".gitbook/assets/image (332).png" alt=""><figcaption><p>Execute PowerShell with HTTP</p></figcaption></figure>

* [HTTP Endpoints](https://docs.powershelluniversal.com/api/endpoints)
* [Custom Responses](https://docs.powershelluniversal.com/api/endpoints#returning-custom-responses)
* [Token-Based Authentication](https://docs.powershelluniversal.com/config/security/app-tokens)
* [Rate Limiting](https://docs.powershelluniversal.com/api/rate-limiting)
* [Large File Support](https://docs.powershelluniversal.com/api/endpoints#processing-files)
* [Open API Documentation](https://docs.powershelluniversal.com/api/endpoints#documenting-apis)
* [File Hosting](https://docs.powershelluniversal.com/platform/published-folders)

## **Automation**

Execute, schedule, secure and audit scripts in an easy-to-use, web-interface.

<figure><img src=".gitbook/assets/image (345).png" alt=""><figcaption><p>Run PowerShell Scripts</p></figcaption></figure>

* [Scheduling](https://docs.powershelluniversal.com/automation/schedules)
* [Run As Support](https://docs.powershelluniversal.com/automation/scripts#running-a-script-as-another-user)
* [Mutliple Environments](https://docs.powershelluniversal.com/config/environments)
* [Automatic Form Generation](https://docs.powershelluniversal.com/automation/scripts#running-a-script-with-parameters)
* [Feedback Integration](https://docs.powershelluniversal.com/automation/jobs#feedback)
* [Pipeline Output](https://docs.powershelluniversal.com/automation/jobs#view-job-pipeline-output)
* [Event Triggers](https://docs.powershelluniversal.com/automation/triggers)
* [Concurrency Controls](https://docs.powershelluniversal.com/automation/scripts#concurrent-jobs)
* [Ad-Hoc Terminals](https://docs.powershelluniversal.com/automation/terminals)

## **User Interfaces**

Build web-based tools for internal users with highly interactive user interfaces that run your scripts.

<figure><img src=".gitbook/assets/image (331).png" alt=""><figcaption><p>Universal Dashboard</p></figcaption></figure>

* [Interactive Apps](apps/building-dashboards.md)
* [Input Forms](https://docs.powershelluniversal.com/userinterfaces/dashboards/components/inputs/form)
* [Customizable Tables](https://docs.powershelluniversal.com/userinterfaces/dashboards/components/data-display/table)
* [Charts](https://docs.powershelluniversal.com/userinterfaces/dashboards/components/data-visualization/charts)
* [Dynamic Regions](https://docs.powershelluniversal.com/userinterfaces/dashboards/components/dynamic-regions)
* [Steppers (Wizards)](https://docs.powershelluniversal.com/userinterfaces/dashboards/components/navigation/stepper)
* [Transitions](https://docs.powershelluniversal.com/userinterfaces/dashboards/components/utilities/transitions)
* [Integration with Scripts and APIs](https://docs.powershelluniversal.com/userinterfaces/pages/form)
* [Extensible Platform](https://docs.powershelluniversal.com/userinterfaces/dashboards/components/building-custom-components)
* [Custom Styling and Branding](https://docs.powershelluniversal.com/userinterfaces/dashboards/themes)

## Hosting

PowerShell Universal is cross-platform and can be hosted on-premises, in the cloud or even on a Raspberry Pi.

<figure><img src=".gitbook/assets/image (358).png" alt=""><figcaption><p>Host in Azure</p></figcaption></figure>

* [Windows, Linux and M](https://docs.powershelluniversal.com/get-started)ac
* [Docker Containers](https://docs.powershelluniversal.com/getting-started/docker)
* [Azure](https://docs.powershelluniversal.com/config/hosting/azure) and [IIS](https://docs.powershelluniversal.com/config/hosting/hosting-iis)
* [Windows Service](https://docs.powershelluniversal.com/getting-started#msi-install-windows)
* [HTTPS](https://docs.powershelluniversal.com/config/hosting#configuring-https)

## Security

Grant role-based access to different aspects of your automation environment with your choice of authentication and authorization integrations.

<figure><img src=".gitbook/assets/image (317).png" alt=""><figcaption><p>Security Settings</p></figcaption></figure>

* [OpenID Connect](https://docs.powershelluniversal.com/config/security/openid-connect)
* [WS-Federation](https://docs.powershelluniversal.com/config/security/ws-federation)
* [Basic Authentication](https://docs.powershelluniversal.com/config/security#forms-authentication)
* [Client Certificate](https://docs.powershelluniversal.com/config/security/client-certificate)
* [SAML2](https://docs.powershelluniversal.com/config/security/saml2)
* [Windows Authentication](https://docs.powershelluniversal.com/config/security#windows-authentication)
* [Script-Based Authorization](https://docs.powershelluniversal.com/config/security#policy-assignment)
* [Claims-Based Authorization](https://docs.powershelluniversal.com/config/security#role-to-claim-mapping)
* [Script Access Controls](https://docs.powershelluniversal.com/config/security/access-controls)
* [Custom and Built-In Roles](https://docs.powershelluniversal.com/config/security#built-in-roles)

## **Desktop**

Create desktop automation and user interfaces that integrate with features of Windows.

* [File Associations](https://docs.powershelluniversal.com/v/v3/desktop/file-associations)
* [Hotkeys](https://docs.powershelluniversal.com/v/v3/desktop/hotkeys)
* [Protocol Handlers](https://docs.powershelluniversal.com/v/v3/desktop/protocol-handlers)
* [System Events](https://docs.powershelluniversal.com/v/v3/desktop/system-events)
* [User Interfaces](https://docs.powershelluniversal.com/v/v3/desktop/pages)

## Development

Take advantage of rich development tools such as IntelliSense, code formatting, error checking and debugger integration without leaving your browser.

<figure><img src=".gitbook/assets/image (189).png" alt=""><figcaption><p>Development Tools in PowerShell Universal</p></figcaption></figure>

* [Rich Editing Experience](https://docs.powershelluniversal.com/platform/editor)
* [Code-First Configuration](https://docs.powershelluniversal.com/config/repository)
* [Debugging Tools](https://docs.powershelluniversal.com/debugging/debugging-scripts#integrated-debugger)
* [PowerShell Module](https://www.powershellgallery.com/packages/Universal)
* [Management API](https://docs.powershelluniversal.com/config/management-api)
* [Visual Studio Code Extension](https://docs.powershelluniversal.com/visual-studio-code-extension)
* [Performance Profiler](https://docs.powershelluniversal.com/debugging/profiling)
* [Desktop Mode](https://docs.powershelluniversal.com/platform/desktop-mode)
* [Hotkeys](https://docs.powershelluniversal.com/platform/desktop-mode/hotkeys)

## Platform

Configure the platform to meet the needs of your environment.

<figure><img src=".gitbook/assets/image (137).png" alt=""><figcaption><p>Module Management</p></figcaption></figure>

* [PowerShell 7 Support](https://docs.powershelluniversal.com/config/environments)
* [Windows PowerShell Support](https://docs.powershelluniversal.com/config/environments)
* [PowerShell Modules](https://docs.powershelluniversal.com/platform/modules)
* [Variables](https://docs.powershelluniversal.com/platform/variables)
* [Password and Secret Management](https://docs.powershelluniversal.com/platform/variables#vaults)
* [Git Integration](https://docs.powershelluniversal.com/config/git)
* [Application Insights Integration](https://docs.powershelluniversal.com/platform/monitoring)

## Community

Join the growing community of users managing their automation environments with PowerShell Universal.

<figure><img src=".gitbook/assets/image (308).png" alt=""><figcaption><p>Community Forums</p></figcaption></figure>

* [Forums](https://forums.ironmansoftware.com/)
* [Discord](https://discord.gg/tQMEYwbGVn)
* [Issue Tracker](https://github.com/ironmansoftware/issues)

## Licensing

Universal is licensed per server. Visit our [website for more information ](https://ironmansoftware.com/powershell-universal/)on pricing.

Many features of PowerShell Universal are [free](licensing.md#licensed-features).
