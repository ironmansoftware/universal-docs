---
description: Iframe component for PowerShell Universal pages.
---

# iFrame

{% hint style="info" %}
Available in PowerShell Universal 2.5 or later.
{% endhint %}

Iframes provide the ability to nest another website within the page. The is especially useful if you wish to embed a dashboard within a page.&#x20;

## Embed a Dashboard in a Page

To embed a dashboard in a page, assume we have a dashboard that is defined such as this. This dashboard returns a table of services. It uses the `-Blank` parameter on `New-UDPage` to remove the header. This dashboard is configured with a base URL of `/embed`

```
New-UDDashboard -Title "Services" -Pages @(
    New-UDPage -Name 'Table' -Content {
        New-UDTable -Data (Get-Service)
    } -Blank
)
```

Add a new IFrame component to the page and within the properties of the page, set the URL to the base URL of the dashboard.&#x20;

![](<../../.gitbook/assets/image (298) (1) (1) (1) (1).png>)

When the page loads, it will load the dashboard and display it within the page.&#x20;

![](<../../.gitbook/assets/image (296) (1) (1).png>)

### Limitations

When you embed multiple dashboards within a page they will be treated an individual dashboards and will not communicate event handling code. This means that display toasts and modals will appear within the IFrame and not in the parent code.&#x20;
