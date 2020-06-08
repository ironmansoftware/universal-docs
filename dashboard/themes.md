# Themes

{% hint style="info" %}
This is documentation for the upcoming and unreleased 1.2 version. 
{% endhint %}

Universal Dashboard v3 is built on Material UI. Material UI provides a [built-in theme system ](https://material-ui.com/customization/theming/)that UD now takes advantage of. You can utilize this theme system by providing a hashtable of options to the `New-UDDashboard` 's `-Theme` parameter. 

Here's an example of changing the theme's main color. 

```text
$Theme = @{
    palette = @{
        primary = @{
            main = '#111111'
        }
    }
}
New-UDDashboard -Theme $Theme -Title 'Hello' -Content {
    New-UDButton -Text "Test " -OnClick {
        Show-UDToast -Message 'HEllo'
    }
}
```

For a full list of options available for the theme system, you can look at the [default theme for Material UI](https://material-ui.com/customization/default-theme/).

