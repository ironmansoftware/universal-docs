---
description: Define static HTML using Universal Dashboard.
---

# HTML

You can define static HTML using `New-UDHtml`. This cmdlet does not create React components but rather allows you to define static HTML. Any valid HTML string is supported.

The following creates an unordered list.

```text
New-UDHtml -Markup "<ul><li>First</li><li>Second</li><li>Third</li></ul>"
```

