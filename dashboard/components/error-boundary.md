---
description: Error boundary component for Universal Dashboard.
---

# Error Boundary

The `New-UDErrorBoundary` component is used for isolating portions of a dashboard to contain components that may throw an error. Many Universal Dashboard components use the error boundary component internally. 

If you'd like to isolate a portion of your dashboard to prevent the entire page from failing to load, you can use the following syntax. 

```PowerShell
New-UDErrorBoundary -Content {
    throw "Oh no!"
}
```

If any error is thrown from the content, you will see an error such as thing. 

![](../../.gitbook/assets/image%20%28173%29.png)

