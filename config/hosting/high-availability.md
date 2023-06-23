---
description: PowerShell Universal high availability configuration.
---

# High Availability

PowerShell Universal can be configured for high availability ("HA") by using a combination of SQL server persistence and a load balancer to ensure that both the front end tools, such as dashboards are accessible and back-end tools, such as jobs, continue to run.&#x20;

![](<../../.gitbook/assets/image (149).png>)

## Persistence Configuration

We recommend taking advantage of [SQL persistence](../persistence.md#sql) to ensure that all nodes within your cluster share the same data in regards to job queues, app tokens and identities within your system. Each node should be configured with the same SQL server connection string.&#x20;

As jobs run, users login and app tokens are created, the SQL server will be used to store this information and will be shared across nodes.&#x20;

## Source Control Configuration

We recommend using [git synchronization](../git.md) to store and version control the PowerShell configuration scripts used to manage the PowerShell Universal nodes. One-way git sync may be preferred as the nodes will then be read-only and pull configurations after they have been merged to your production branch. Each node pulls the configuration files on a configurable interval (defaults to 1 minute). Storing git configuration settings in the database is desired as it requires less configuration per node.&#x20;

## Load Balancing

PowerShell Universal supports the use of load balancers such as F5 and nginx. There are some requirements that must be met when using load balancers.&#x20;

* Persistent (sticky) sessions are required by dashboards
* Web socket support is required by the admin console and dashboards

To aid with load balancing; you can use the `/api/v1/status` endpoint for your nodes. The endpoint will return status codes based on the current state of the node. `200` means the node is online and ready to receive requests. Servers running in maintenance mode will return `503`. Servers that failed to start due to a configuration error, will return `500`. Servers with dashboards that failed to start will also return `500`.&#x20;

## Maintenance Mode

You can set your nodes into Maintenance Mode by clicking Platform \ Computers and checking the maintenance mode option. Once maintenance mode is enabled, the `/api/v1/status` endpoint will begin returning `503`. This should be configured to disable traffic being routed to the node while maintenance is performed.&#x20;

## Limitations&#x20;

There currently are some limitations to highly available PowerShell Universal clusters.

### Multi-Node Caching

Caching performed using `$Cache` or `Set-PSUCache` is currently limited to the single node that is performing these operations as they are stored in memory on the system. We recommend an external cache, such as Redis, if you wish to cache data across nodes.&#x20;

### Multi-Node Dashboard Broadcast

Multi-Node dashboard broadcast messages are currently not supported. Using cmdlets like `Show-UDToast -Broadcast` will cause a toast modal to be shown to all connected users of the current node but will not be broadcast to the dashboards across all nodes.&#x20;

