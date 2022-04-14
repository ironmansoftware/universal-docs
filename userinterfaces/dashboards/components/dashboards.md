---
description: Dashboards are the root component for a web site.
---

# Dashboards

Dashboards are the root component for all components and pages.&#x20;

### Basic Dashboards

The basic dashboard requires a title and content.&#x20;

```powershell
New-UDDashboard -Title 'Dashboard' -Content {

}
```

### Dashboard with Pages

Pages allow you to organize your dashboard into separate URLs under the same dashboard. You can learn more about pages here.&#x20;

The below dashboard will have pages available at `/page1` and `/page2`.&#x20;

```powershell
New-UDDDashboard -Title 'Pages' -Pages @(
     New-UDPage -Name 'Page1' -Content {}
     New-UDPage -Name 'Page2' -Content {}
)
```

### Custom Not Found Page

When using multiple pages, users may access a page that does not exist. By default, a standard not found page will be displayed. To customize the not found page, use the `-PageNotFound` parameter.

```powershell
New-UDDDashboard -Title 'Pages' -Pages @(
     New-UDPage -Name 'Page1' -Content {}
     New-UDPage -Name 'Page2' -Content {}
) -PageNotFound {
   New-UDTypograhy 'Not Found'
}
```

### Custom Not Authorized Page

By default, the Not Found page will be displayed when a user is not authorized to view it. If you customize the Not Authorized page, this will be displayed instead.&#x20;

```powershell
New-UDDDashboard -Title 'Pages' -Pages @(
     New-UDPage -Name 'Page1' -Content {}
     New-UDPage -Name 'Page2' -Content {} -Role Administrator
) -NotAuthorized {
   New-UDTypograhy 'Not Authorized'
}
```
