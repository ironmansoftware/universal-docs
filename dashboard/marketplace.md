---
description: The page shows how to use the Universal Dashboard marketplace.
---

# Marketplace

The [Universal Dashboard Marketplace](https://marketplace.universaldashboard.io/) is a PowerShell Gallery module aggregator. It synchronizes with the PowerShell Gallery on an hourly basis to find modules that can be used with Universal Dashboard. 

## Installing Components from the Gallery 

### Automatic Install from the Marketplace

Within PowerShell Universal, you can access the Universal Dashboard Marketplace by navigating to the Dashboard \ Components page and clicking the Marketplace button. This will allow you to browse the Marketplace for components for your dashboard. If you want to install a component, you can click the install button.

![](../.gitbook/assets/image%20%28104%29.png)

Once installed, the component will be listed on the Dashboard \ Components page. 

image 

![](../.gitbook/assets/image%20%28106%29.png)

To add the component to  a dashboard, navigate to the Dashboard \ Dashboards page, click Info and go to the Components tab. On the top right, click the component button.

image

![](../.gitbook/assets/image%20%28103%29.png)

The drawer will show which components are already added and which components can be added. Click the add button to activate the component for the dashboard. 

![](../.gitbook/assets/image%20%28105%29.png)

### Manual Install from the PowerShell Gallery

You can install any of the components from the Marketplace by using the `Install-Module` or `Save-Module` cmdlets provided by `PowerShellGet`. Since the components are just listed on the PowerShell Gallery, you'll be able to use their module name during install. 

```text
Install-Module UniversalDashboard.Helmet
```

Depending on how the components were installed, you may need to import the module in your dashboard file.

```text
Import-Module UniversalDashboard.Helmet
```

## Publishing to the Universal Dashboard Marketplace

You can follow the directions on the [Building Custom Components](components/building-custom-components.md#publishing-to-the-marketplace) page on how to publish components to the Universal Dashboard Marketplace. 

