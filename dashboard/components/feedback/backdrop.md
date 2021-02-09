---
description: Backdrop component for Universal Dashboard.
---

# Backdrop

{% hint style="warning" %}
This component will be available in a future version of Universal Dashboard.
{% endhint %}

The backdrop component places an overlay over the drop of the entire page. It's useful for displaying loading states. 

## Basic Backdrop

To create a basic backdrop, you can use the `New-UDBackdrop` cmdlet and include content to show within the backdrop. The content will be centered on the page. To show the backdrop, use the `-Open` switch parameter. 

```text
New-UDBackdrop -Content {
    New-UDTypography -Text "Loading..." -Variant h2
} -Open 
```

![Backdrop component](../../../.gitbook/assets/image%20%28214%29.png)

## OnClick Handler

The backdrop provides an `-OnClick` handler that you can use to close the backdrop when clicked. You can use `Set-UDElement` to open and close the backdrop.

```text
New-UDBackdrop -Id 'backdrop' -Content {
    New-UDTypography -Text "Loading..." -Variant h2
} -Open -OnClick {
    Set-UDElement -Id 'backdrop' -Properties @{
        open = $false
    }
}
```

