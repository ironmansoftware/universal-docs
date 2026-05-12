---
description: PowerShell Universal high availability configuration.
---

# High Availability

PowerShell Universal can be configured for high availability ("HA") by using a combination of SQL server persistence and a load balancer to ensure that both the front end tools, such as dashboards are accessible and back-end tools, such as jobs, continue to run.

![](<../../.gitbook/assets/image (149).png>)

## Persistence Configuration

We recommend taking advantage of [SQL persistence](../persistence.md#sql) (or PostgreSQL) to ensure that all nodes within your cluster share the same data in regard to job queues, app tokens and identities within your system. Each node should be configured with the same SQL server connection string.

As jobs run, user's login and app tokens are created, the SQL server will be used to store this information and will be shared across nodes.

## Source Control Configuration

We recommend using [git synchronization](../git.md) to store and version control the PowerShell configuration scripts used to manage the PowerShell Universal nodes. One-way git sync may be preferred as the nodes will then be read-only and pull configurations after they have been merged to your production branch. Each node pulls the configuration files on a configurable interval (defaults to 1 minute). Storing git configuration settings in the database is desired as it requires less configuration per node.

## Load Balancing

PowerShell Universal supports the use of load balancers such as F5 and nginx. There are some requirements that must be met when using load balancers.

* Persistent (sticky) sessions are required by the admin console and apps
* Web socket support is required by the admin console and apps

To aid with load balancing; you can use the `/api/v1/status` endpoint for your nodes. The endpoint will return status codes based on the current state of the node. `200` means the node is online and ready to receive requests. Servers running in maintenance mode will return `503`. Servers that failed to start due to a configuration error, will return `500`. Servers with apps that failed to start will also return `500`.

## Status APIs

### &#x20;`/api/v1/status`

You can set your nodes into Maintenance Mode by clicking Platform \ Computers and checking the maintenance mode option. Once maintenance mode is enabled, the `/api/v1/status` endpoint will begin returning `503`. This should be configured to disable traffic being routed to the node while maintenance is performed. This endpoint will also return 5xx if the following is true:

* Computer is in a startup error status
* Computer is in maintenance mode
* Critical app is in a startup failed state
* API endpoints are configured but are not running properly

### `/api/v2/status`

The v2 status API will return a `503` for additional reasons. They include:

* Any computer in the cluster is offline but not in maintenance mode
* Git sync is failing to pull changes on any node
* API endpoints are configured but are not running properly

## Limitations

There currently are some limitations to highly available PowerShell Universal clusters.

### Multi-Node Caching

Caching performed using `$Cache` is limited to a single process on a single node. For example, each app running outside the integrated environment will have its own cache.

`Set-PSUCache` will not share data across nodes if `-Persist` is not specified. To ensure all nodes have the same data include this switch.

### Multi-Node App Broadcast

Multi-Node app broadcast messages are currently not supported. Using cmdlets like `Show-UDToast -Broadcast` will cause a toast modal to be shown to all connected users of the current node but will not be broadcast to the apps across all nodes.
