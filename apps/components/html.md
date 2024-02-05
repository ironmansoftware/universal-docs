---
description: Define static HTML using Univeral apps.
---

# HTML

You can define static HTML using `New-UDHtml`. This cmdlet does not create React components but rather allows you to define static HTML. Any valid HTML string is supported.

The following creates an unordered list.

```powershell
New-UDHtml -Markup "<ul><li>First</li><li>Second</li><li>Third</li></ul>"
```

## API

[**New-UDHtml**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDHtml.txt)
