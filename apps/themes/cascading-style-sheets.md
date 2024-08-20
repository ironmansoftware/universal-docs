---
description: Use cascading style sheets with PowerShell Universal.
---

# Cascading Style Sheets

You can use a cascading style sheet (CSS) by add a `.css` file to a published folder and then passing it to the `-Stylesheets` parameter for `New-UDDashboard`.

For example, the `dashboard.ps1` file would look like this.

```powershell
New-UDDashboard -Title "Server Monitor" -Content {


} -Stylesheets @("/assets/theme.css")
```

You could then setup a published folder to provide the assets route. This is what the contents of `publishedFolders.ps1` will look like.

```powershell
New-PSUPublishedFolder -RequestPath "/assets" -Path "C:\assets"
```

Within the `C:\assets` folder, you can place any assets you'd like to access on the `/assets` route.

![Assets folder](<../../.gitbook/assets/image (179).png>)

You can then create a style sheet to manipulate whatever portion of the dashboard you'd like.

```css
.ud-dashboard > div {
    background-image: url("/assets/image.jpeg");
}
```

This produces a dashboard with a background image of Austin the dog sleeping in a pile of dirt.

![](<../../.gitbook/assets/image (380).png>)

## Determining the Correct Class Names

Every Material UI component has a series of global class names that you can use to apply styles throughout your dashboard. To determine the correct class names, you can view the a particular component's API documentation. There is a list of the global class names that apply to that component.

For example, here is the [CSS documentation for the Alert component](https://material-ui.com/api/alert/#css).

Within your CSS file, you can use these class names to override styles throughout your dashboard. If you wanted to set all success alerts to have a red background, you could create a CSS file like this.

```css
.MuiAlert-standardSuccess { background-color: red !important;  }
```
