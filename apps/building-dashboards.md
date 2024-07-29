---
description: Apps are the root component for your web page.
---

# Apps

Here's an example of a simple app that displays some text.

```powershell
New-UDApp -Title 'My New Dashboard' -Content {
    New-UDTypography -Text 'Hello!'
}
```

### New-UDApp

The top-level cmdlet for dashboards is `New-UDApp`. You need to call it when returning an app. You can use it with or without pages.

#### Content

The content of the app is a series of components to display on the page. It's a script block that will return all the components in the order they will be rendered on the page. You can use the Grid component to layout items and display things like text with typography.

```powershell
New-UDApp -Title 'My New Dashboard' -Content {
    New-UDTypography -Text 'Hello!'
}
```

#### Header Customization

You can customize the header of the app using several parameters.

To change the navigation layout, use the `-Navigation` and `-NavigationLayout` parameters.

```powershell
New-UDApp -Content {
} -Navigation (
    New-UDList -Children {
        New-UDListItem -Label "Home"
        New-UDListItem -Label "Getting Started" -Children {
            New-UDListItem -Label "Installation" -OnClick {}
            New-UDListItem -Label "Usage" -OnClick {}
            New-UDListItem -Label "FAQs" -OnClick {}
            New-UDListItem -Label "System Requirements" -OnClick {}
            New-UDListItem -Label "Purchasing" -OnClick {}
        }
    }
) -NavigationLayout permanent
```

### Components

Components are the individual widgets that you can place on you app. There are components for displaying data, taking user input, adding text and images and more. Components can be downloaded as PowerShell modules and added to your app.

Components are be caused using the standard verb-name syntax for any PowerShell cmdlet.

```powershell
New-UDPage -Content {
    New-UDTextbox
}
```

Learn more about [components here](building-dashboards.md#components).

### Pages

You can specify multiple pages within an app. Each page defines a route. As for v3, all pages are dynamic. PowerShell will execute on each page load to render the new page. Since UD is a single page application, the web browser does not need to refresh the entire web page when navigating between the different app pages.

```powershell
$Pages = @()
$Pages += New-UDPage -Name 'My Home Page' -Content {}
$Pages += New-UDPage -Name 'Diagnostics' -Content {}
New-UDApp -Pages $Pages -Title 'Dashboard'
```

Learn more about [Pages here](building-dashboards.md#pages).

### Built-in Variables

Built-in variables can be found on the [variables page](../platform/variables.md#dashboards).

### Debugging

{% hint style="info" %}
You can also use the [Debugging Tools](../development/debugging-scripts.md#integrated-debugger) with apps.
{% endhint %}

When building an app, you will likely run into issues with cmdlet calls or syntax. Apps will auto reload as you make changes to the app files. If an app fails to start, you can navigate to the admin page, click Apps and click the Info button next to your app.

The Log tab will show all the logging coming from the PowerShell execution from within in your app. This should allow you to easily see errors and warnings coming from your app.

You can use `Write-Debug` to add additional log messages to your app. To enable debug logging, you will have to set the `$DebugPreference` variable at the top of your app script.

```powershell
$DebugPreference = 'Continue'
```

### Menu

You can customize the appmenu by using the `-Menu` parameter.

```powershell
New-UDApp -Title 'App' -Content {

} -Menu {
    New-UDMenuItem -Text 'Profile' -OnClick {
        Show-UDModal -Content {
            New-UDTypography -Text 'Welcome to your profile!'
        }
    }
}
```
