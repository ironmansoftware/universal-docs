---
description: Error boundary component for Universal Dashboard.
---

# Error Boundary

{% hint style="warning" %}
This documentation for an upcoming version of PowerShell Universal. You can download [nightly builds](https://imsreleases.z19.web.core.windows.net/) if you want to try it out.
{% endhint %}

The `New-UDErrorBoundary` component is used for isolating portions of a dashboard to contain components that may throw an error. Many Universal Dashboard components use the error boundary component internally. 

If you'd like to isolate a portion of your dashboard to prevent the entire page from failing to load, you can use the following syntax. 

```text
New-UDErrorBoundary -Content {
    throw "Oh no!"
}
```

If any error is thrown from the content, you will see an error such as thing. 

![](../../.gitbook/assets/image%20%28173%29.png)

