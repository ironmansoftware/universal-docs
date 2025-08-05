---
description: Host Yet Another Reverse Proxy (YARP).
---

# YARP

**Identifier:** `PowerShellUniversal.Plugins.YARP`

[YARP](https://microsoft.github.io/reverse-proxy/articles/index.html) (Yet Another Reverse Proxy) is a Microsoft project that allows ASP.NET Core applications to act as reverse proxies. PowerShell Universal only exposes this configuration but does not extend it in many regards. You can use [App Settings ](../../config/settings.md)to configure the proxy and starting the PSU service will enable the YARP functionality. Follow the [YARP articles](https://microsoft.github.io/reverse-proxy/articles/index.html) to understand how to configure the service.

The one extension that we do provide into YARP is the ability to specify a PSU role that is required for a particular proxy route. For example, the following would enforce the Administrator role.

```json
{
    "ReverseProxy": {
        "Routes": {
            "route1": {
                "ClusterId": "cluster1",
                "AuthorizationPolicy": "AdministratorRolePolicy",
                "Match": {
                    "Path": "/code/{**catch-all}"
                },
                "Transforms": [
                    {
                        "PathRemovePrefix": "/code"
                    }
                ]
            }
        },
        "Clusters": {
            "cluster1": {
                "Destinations": {
                    "destination1": {
                        "Address": "http://localhost:8080"
                    }
                }
            }
        }
    }
}
```

You can replace the `Administrator` portion of the policy name to enforce a different role. For example: `ExecutorRolePolicy`.
