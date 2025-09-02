---
description: Define static HTML using Univeral apps.
---

# HTML

You can define static HTML using `New-UDHtml`. This cmdlet does not create React components but rather allows you to define static HTML. Any valid HTML string is supported.

The following creates an unordered list.

```powershell
New-UDHtml -Markup "<ul><li>First</li><li>Second</li><li>Third</li></ul>"
```

### Modifying the \<head> tag

You can use the `New-UDHelmet` component to add new tags to the \<head> of the HTML document. This is useful for loading custom JavaScript or CSS libraries.&#x20;

```powershell
New-UDHelmet -Tag 'script' -Attributes @{
    src = 'https://unpkg.com/mermaid@8.1.0/dist/mermaid.min.js'
} 
```

## API

* [New-UDHtml](../../cmdlets/New-UDHtml.txt)
* [New-UDHelmet](../../cmdlets/New-UDHelmet.txt)

