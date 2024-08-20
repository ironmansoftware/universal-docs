---
description: Error boundary component for apps.
---

# Error Boundary

The `New-UDErrorBoundary` component is used for isolating portions of a dashboard to contain components that may throw an error. Many app components use the error boundary component internally.

If you'd like to isolate a portion of your app to prevent the entire page from failing to load, you can use the following syntax.

```powershell
New-UDErrorBoundary -Content {
    throw "Oh no!"
}
```

If any error is thrown from the content, you will see an error such as thing.

![](<../../../.gitbook/assets/image (58).png>)

## API

[**New-UDErrorBoundary**](https://github.com/ironmansoftware/universal-docs/blob/master/cmdlets/New-UDErrorBoundary.txt)
