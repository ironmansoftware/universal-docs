---
description: The ultimate command center for your PowerShell environment.
---

# ❓ About

<figure><img src=".gitbook/assets/image (332) (1).png" alt=""><figcaption><p>PowerShell Universal Admin Console</p></figcaption></figure>

PowerShell Universal provides a centralized location to store and run scripts, build modules, expose REST APIs and share them with end users via automatic or custom user interfaces, setup schedules and more.

## **APIs**

Transform your PowerShell scripts into RESTful HTTP and WebSocket APIs for seamless integration across platforms. Leverage OpenAPI provide documentation and additional automation opportunities.

<figure><img src=".gitbook/assets/image (332) (1).png" alt=""><figcaption><p>Execute PowerShell with HTTP</p></figcaption></figure>

* [HTTP Endpoints](https://docs.powershelluniversal.com/api/endpoints)
* [Custom Responses](https://docs.powershelluniversal.com/api/endpoints#returning-custom-responses)
* [Token-Based Authentication](https://docs.powershelluniversal.com/config/security/app-tokens)
* [Rate Limiting](https://docs.powershelluniversal.com/api/rate-limiting)
* [Large File Support](https://docs.powershelluniversal.com/api/endpoints#processing-files)
* [Open API Documentation](https://docs.powershelluniversal.com/api/endpoints#documenting-apis)
* [File Hosting](https://docs.powershelluniversal.com/platform/published-folders)
* [Event Hubs](api/event-hubs.md)

## **Automation**

Streamline your automation with an intuitive web interface for executing, scheduling, securing, and auditing PowerShell scripts. Effortlessly manage tasks and access in-browser terminals to maximize efficiency and control in your automation workflows.

<figure><img src=".gitbook/assets/image (345).png" alt=""><figcaption><p>Run PowerShell Scripts</p></figcaption></figure>

* [Scheduling](https://docs.powershelluniversal.com/automation/schedules)
* [Run As Support](https://docs.powershelluniversal.com/automation/scripts#running-a-script-as-another-user)
* [Multiple Environments](https://docs.powershelluniversal.com/config/environments)
* [Automatic Form Generation](https://docs.powershelluniversal.com/automation/scripts#running-a-script-with-parameters)
* [Feedback Integration](https://docs.powershelluniversal.com/automation/jobs#feedback)
* [Pipeline Output](https://docs.powershelluniversal.com/automation/jobs#view-job-pipeline-output)
* [Event Triggers](https://docs.powershelluniversal.com/automation/triggers)
* [Concurrency Controls](https://docs.powershelluniversal.com/automation/scripts#concurrent-jobs)
* [Ad-Hoc Terminals](https://docs.powershelluniversal.com/automation/terminals)
* [Pester Test Support](automation/tests.md)

## **Apps**

Create fully customizable, interactive web apps tailored for your internal users using PowerShell. With over 70 versatile controls and seamless integration to other PowerShell modules and scripts, you can build powerful interfaces to enhance productivity and collaboration.

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

* [Windows, Linux and Mac](https://docs.powershelluniversal.com/get-started)
* [Docker Containers](https://docs.powershelluniversal.com/getting-started/docker)
* [Azure](https://docs.powershelluniversal.com/config/hosting/azure)
* [IIS](https://docs.powershelluniversal.com/config/hosting/hosting-iis)
* [Windows Service](https://docs.powershelluniversal.com/getting-started#msi-install-windows)
* [HTTPS](https://docs.powershelluniversal.com/config/hosting#configuring-https)

## Security

PowerShell Universal is a versatile, cross-platform solution that adapts to your hosting needs. Deploy seamlessly on AWS, Azure, IIS, or your on-premises infrastructure—even on compact devices like a Raspberry Pi. Flexibility meets power for automation anywhere.

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

## Development

PowerShell Universal delivers a seamless development experience with built-in tools like IntelliSense, syntax highlighting, error checking, formatting, and debugging—all accessible directly from your browser. Enhance productivity further with a dedicated VS Code extension and integrated Git support for streamlined version control.

<figure><img src=".gitbook/assets/image (91) (1).png" alt=""><figcaption><p>Development Tools in PowerShell Universal</p></figcaption></figure>

* [Rich Editing Experience](https://docs.powershelluniversal.com/platform/editor)
* [Code-First Configuration](https://docs.powershelluniversal.com/config/repository)
* [Debugging Tools](https://docs.powershelluniversal.com/debugging/debugging-scripts#integrated-debugger)
* [PowerShell Module](https://www.powershellgallery.com/packages/Universal)
* [Management API](https://docs.powershelluniversal.com/config/management-api)
* [Visual Studio Code Extension](https://docs.powershelluniversal.com/visual-studio-code-extension)
* [Performance Profiler](https://docs.powershelluniversal.com/debugging/profiling)

## Platform

With support for PowerShell 7 and Windows PowerShell, seamless integration with PowerShell modules, and powerful tools for variable and secret management, it adapts to your needs. Enjoy multilingual support, compatibility with multiple database types (SQLite, SQL Server, PostgreSQL), and built-in high availability and load balancing for enterprise-grade scalability.

<figure><img src=".gitbook/assets/image (137).png" alt=""><figcaption><p>Module Management</p></figcaption></figure>

* [PowerShell 7 Support](https://docs.powershelluniversal.com/config/environments)
* [Windows PowerShell Support](https://docs.powershelluniversal.com/config/environments)
* [PowerShell Modules](https://docs.powershelluniversal.com/platform/modules)
* [Variables](https://docs.powershelluniversal.com/platform/variables)
* [Password and Secret Management](https://docs.powershelluniversal.com/platform/variables#vaults)
* [Git Integration](https://docs.powershelluniversal.com/config/git)
* [Application Insights Integration](https://docs.powershelluniversal.com/platform/monitoring)

## Community

Join the thriving PowerShell Universal community and connect with like-minded professionals. Participate in our active forum for support and collaboration, explore our open-source gallery of pre-made solutions, and stay informed with our transparent roadmap and bug tracker.

<figure><img src=".gitbook/assets/image (308).png" alt=""><figcaption><p>Community Forums</p></figcaption></figure>

* [Forums](https://forums.ironmansoftware.com/)
* [Issue Tracker](https://github.com/ironmansoftware/issues)
* [Discord](https://discord.gg/Sb5ngcjkj4)

## Licensing

Universal is licensed per server. Visit our [website for more information ](https://ironmansoftware.com/powershell-universal/)on pricing.

Many features of PowerShell Universal are [free](licensing.md#licensed-features).
