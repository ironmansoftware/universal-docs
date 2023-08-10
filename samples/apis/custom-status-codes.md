---
description: This sample shows how to define custom status codes for an API endpoint.
---

# Custom Status Codes

```powershell
New-PSUEndpoint -Url '/status' -Endpoint {
    New-PSUApiResponse -StatusCode 418
}
```

This sample returns the [I am a teapot status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/418).&#x20;
