---
description: >-
  Configuration information for hosting PowerShell Universal behind a reverse
  proxy.
---

# Reverse Proxy

Reverse proxies allow for configuration of features such as TLS, header rewriting, caching and load balancing. Some popular reverse proxies include IIS, Apache and NGINX.

Each of these systems capture HTTP traffic and forward it to a backend web server, like PowerShell Universal. There are some considerations that should be made when configuring a reserve proxy in front of PowerShell Universal.

## WebSocket Support

PowerShell Universal requires WebSocket support to provide all the features available within the platform. Without WebSocket support, apps will not function, and notifications will not be presented in real time.

Depending on your proxy, you may need to configure WebSocket support.

* [IIS WebSocket Protocol Support](https://learn.microsoft.com/en-us/iis/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)
* [NGINX WebSocket proxying](https://nginx.org/en/docs/http/websocket.html)

## Forwarded Headers

When a web server is behind a reverse proxy, it's likely that the external host name, protocol and port will differ from the proxy itself. For example, PowerShell Universal will be listening on port 5000, on HTTP and based on a specific IP address (or loopback) rather than a DNS name.

```
https://www.proxyaddress.com -> http://localhost:5000
```

This can cause problems with URL redirects like the ones used in [OpenID Connect](../../security/enterprise-security/openid-connect.md) authentication flows. PowerShell Universal needs to be able to correctly formulate the redirect URL for the authentication flow. Without knowing what the actual host name, port or protocol used by the end user, invalid URLs can be generated causing the flow to fail.

By default, PowerShell Universal automatically hands [forwarded headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded). The following headers are automatically processed.

* X-Forwarded-For
* X-Forwarded-Host
* X-Forwarded-Proto

This allows PowerShell Universal to create the proper redirect URLs for authentication flows.

Reserve proxies may require configuration to properly send these headers.

* IIS Automatically configures forwarded headers.
* [NGINX Forwarded Headers](https://www.nginx.com/resources/wiki/start/topics/examples/forwarded/)
* [Apache mod\_proxy](https://httpd.apache.org/docs/2.4/mod/mod\_proxy.html#x-headers)
* [CloudFlare HTTP request headers](https://developers.cloudflare.com/fundamentals/get-started/reference/http-request-headers/#x-forwarded-for)
