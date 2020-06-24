---
description: Typography component for Universal Dashboard
---

# Typography

Use typography to present your design and content as clearly and efficiently as possible.

Too many type sizes and styles at once can spoil any layout. A typographic scale has a limited set of type sizes that work well together along with the layout grid.

## All Typography Types

```text
@("h1", "h2", "h3", "h4", "h5", "h6", "subtitle1", "subtitle2", "body1", "body2", 
"caption", "button", "overline", "srOnly", "inherit", 
"display4", "display3", "display2", "display1", "headline", "title", "subheading") | ForEach-Object {
    New-UDTypography -Variant $_ -Text $_ -GutterBottom
    New-UDElement -Tag 'p' -Content {}
}
```

