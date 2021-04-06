# Building Dashboards

{% hint style="info" %}
We recommend installing the [PowerShell Universal Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=ironmansoftware.powershell-universal). Read more about dashboard development [here](../development.md).
{% endhint %}

When building dashboards, you will pick one of the two built in dashboard frameworks. The components that are available for that framework will different. You can find examples of each of the frameworks at the below links. 

* [Universal Dashboard v2](https://github.com/ironmansoftware/universal-dashboard/tree/master/src/v2/example)
* [Universal Dashboard v3](https://github.com/ironmansoftware/universal-dashboard/tree/master/src/v3/example)

{% hint style="info" %}
All the documentation on this page will be referencing the v3 framework. 
{% endhint %}

Dashboards can contain one or more pages. The simplest dashboard will contain a single page with some content. You can call any PowerShell cmdlet that is available on your machine to populate your dashboard. 

Here's an example of simple dashboard that displays some text. 

```PowerShell
New-UDDashboard -Title 'My New Dashboard' -Content {
    New-UDTypography -Text 'Hello!'
}
```

### Components

Components are the individual widgets that you can place on you dashboard. There are components for displaying data, taking user input, adding text and images and more. Components can be downloaded as PowerShell modules and added to your dashboard. 

Examples of all of the components can be found [on GitHub](https://github.com/ironmansoftware/universal-dashboard/tree/master/src/v3/example/pages).

Components are be caused using the standard verb-name syntax for any PowerShell cmdlet. 

```PowerShell
New-UDPage -Content {
    New-UDTextbox
}
```

### Pages

You can specify multiple pages within a dashboard. Each page defines a route. As for v3, all pages are dynamic. PowerShell will execute on each page load to render the new page. Since UD is a single page application, the web browser does not need to refresh the entire web page when navigating between the different dashboard pages. 

```PowerShell
$Pages = @()
$Pages += New-UDPage -Name 'My Home Page' -Content {}
$Pages += New-UDPage -Name 'Diagnostics' -Content {}
New-UDDashboard -Pages $Pages -Title 'Dashboard'
```

## Built-in Variables

There are several built-in variables that are available in dashboards. 

| Name | Description | Type |
| :--- | :--- | :--- |
| $User | The user name of the logged in user. $Null if authentication is disabled. | String |
| $Roles | The roles that the user has been granted. $Null if authentication is disabled. | String\[\] |
| $RemoteIpAddress | The remote IP address of the connected user. **Only available in the nightly build** | String |
| $RmotePort | The remote port of the connected user. **Only available in the nightly build** | Int |



## Debugging

When building a dashboard you will likely run into issues with cmdlet calls or syntax. Dashboards will auto reload as you make changes to the dashboard files. If a dashboard fails to start, you can navigate to the admin page, click Dashboards and click the Info button next to your dashboard. 

The Log tab will show all the logging coming from the PowerShell execution from within in your dashboard. This should allow you to easily see errors and warnings coming from your dashboard. 

You can use `Write-Debug` to add additional log messages to your dashboard. To enable debug logging, you will have to set the `$DebugPreference` variable at the top of your dashboard script.

```PowerShell
$DebugPreference = 'Continue'
```

