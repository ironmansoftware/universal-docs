---
description: Use cascading style sheets with Universal Dashboard.
---

# Cascading Style Sheets

You can use a cascading style sheet \(CSS\) by add a `.css` file to a published folder and then passing it to the `-Stylesheets` parameter for `New-UDDashboard`. 

For example, the `dashboard.ps1` file would look like this. 

```text
New-UDDashboard -Title "Server Monitor" -Content {


} -Stylesheets @("/assets/theme.css")
```

You could then setup a published folder to provide the assets route. This is what the contents of `publishedFolders.ps1` will look like. 

```text
New-PSUPublishedFolder -RequestPath "/assets" -Path "C:\assets"
```

Within the `C:\assets` folder, you can place any assets you'd like to access on the `/assets` route. 

![Assets folder](../../.gitbook/assets/image%20%28164%29.png)

You can then create a style sheet to manipulate whatever portion of the dashboard you'd like. 

```text
.ud-dashboard > div {
    background-image: url("/assets/image.jpeg") !important;
}
```

This produces a dashboard with a background image of Austin the dog sleeping in a pile of dirt. 

![](../../.gitbook/assets/image%20%28165%29.png)



