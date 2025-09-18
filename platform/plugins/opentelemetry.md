---
description: Send telemetry data to OpenTelemetry.
---

# OpenTelemetry

**Identifier:** `PowerShellUniversal.Plugins.OpenTelemetry`

OpenTelemetry is a collection of APIs, SDKs, and tools. Use it to instrument, generate, collect, and export telemetry data (metrics, logs, and traces) to help you analyze your software’s performance and behavior.

The plugin enables integration with the technology. You can use [App Settings](../../config/settings.md) to configure where to send data. PowerShell Universal currently only exposes a single OTLP endpoint configuration. The below configuration would work with Prometheus.

```json
{    
    "OpenTelemetry": {
        "Otlp": {
            "Endpoint": "http://localhost:9090/api/v1/otlp/v1/metrics"
        }
    }
}
```

### Prometheus&#x20;

You can configure Prometheus to collect PowerShell Universal data by starting it with the OTLP collector enabled.

```powershell
 .\prometheus.exe --web.enable-otlp-receiver
```

Within PowerShell Universal, you will need to specify the `/api/v1/otlp/v1/metrics` URL for the Prometheus server. This example uses Prometheus 3.5.

```powershell
{    
    "OpenTelemetry": {
        "Otlp": {
            "Endpoint": "http://localhost:9090/api/v1/otlp/v1/metrics"
        }
    }
}
```
