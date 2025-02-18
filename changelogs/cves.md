---
description: CVEs for PowerShell Universal.
---

# CVEs

Please report vulnerabilities to Ironman Software. To learn about our vulnerability response policy, [click here](https://ironmansoftware.com/vulnerability-response-policy/).

## CVE-TBD - 2/18/2025 - Incorrect Access Controls

### Description

Due to an authorization issue with the PowerShell Universal v5.3.x's gRPC service registration, a remote attacker can access the server using the Universal PowerShell module without authentication.&#x20;

### CVSS v4.0 Score: 9.8 High

## CVE-2025-26792 - 1/29/2025 - Information disclosure

### Description

Version 4.5.x and 5.x.x are vulnerable to an information disclosure through directory traversal when using PowerShell Universal published folders. Systems that do not have this feature configured, are not affected. If authenticated published folders are configured, the attacker will need to be authenticated.&#x20;

### CVSS v4.0 Score: 5.4 / Medium

This exploit allows an attacker to expose information of the affected system, depending on system configuration.

## CVE-2024-50616 - 10/17/2024 - Privilege escalation and information disclosure

### Description

Version 5.0.0 through 5.0.11 are vulnerable to an exploit that allows an authenticated attacker to elevate their privileges and view job information.

### CVSS v4.0 Score: 7.4 / High

This exploit allows an authenticated attacker to take control of the platform via a vulnerability in the admin console.

###

###
