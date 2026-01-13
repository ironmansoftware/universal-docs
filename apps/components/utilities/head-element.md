---
description: Add head element tags to your pages.
---

# Head Element

You can use the `New-UDHelmet` cmdlet to add `<head>` element tags like `<script>` and `<style>` to your pages. This is useful for including externally hosted JavaScript or CSS.&#x20;

## JavaScript

You can load JavaScript by using the script tag with the `src` attribute. Note, limitations on cross-site resources may be in affect and you may need to adjust the web server configuration to support this.&#x20;

```powershell
New-UDApp -Content {
    New-UDHelmet -Tag 'script' -Attributes @{ src = "https://www.mycdn.com/site.js" } 
}
```

## CSS

You can load CSS using the `link` tag.

```powershell
New-UDHelmet -Tag 'link' -Attributes @{ 
    rel = 'stylesheet' 
    href = "mystylesheet.css"
} 
```

## Styles

You can use a `style` tag to provide styles directly.

```powershell
New-UDHelmet -Tag 'style' -Attributes @{ 
    type = 'text/css' 
} -Children { 
    "body { background-color: 'red'}" 
}
```

## App

You can also load stylesheets and scripts from the app directly.

```powershell
New-UDApp -Content {

} -Stylesheets "mysheet.js" -Scripts "mysite.js"
```
