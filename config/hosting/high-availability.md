---
description: PowerShell Universal high availability configuration.
---

# High Availability

PowerShell Universal can be configured for high availability by using a combination of SQL server persistence and a load balancer to ensure that both the front end tools, such as dashboards are accessible and back end tools, such as jobs, continue to run.&#x20;

## Persistence Configuration

We recommend taking advantage of [SQL persistence](../persistence.md#sql) to ensure that all nodes within your cluster share the same data in regards to job queues, app tokens and identities within your system. Each node should be configured with the same SQL server connection string.&#x20;

As jobs run, users login and app tokens are created, the SQL server will be used to store this information and will be shared across nodes.&#x20;

## Source Control Configuration

We recommend using [git synchronization](../git.md) to store and version control the PowerShell configuration scripts used to manage the PowerShell Universal nodes. One-way git sync may be preferred as the nodes will then be read-only and pull configurations after they have been merged to your production branch. Each node pulls the configuration files on a configurable interval (defaults to 1 minute). Storing git configuration settings in the database is desired as it requires less configuration per node.&#x20;

## Load Balancing

PowerShell Universal supports the use of load balancers such as F5 and nginx. There are some requirements that must be met when using load balancers.&#x20;

* Persistent (sticky) sessions are required by dashboards
* Web socket support is required by the admin console and dashboards

## Limitations&#x20;

There currently are some limitations to highly available PowerShell Universal clusters.&#x20;

### Single Job Queue

The entire cluster uses a single job queue. This means that running a schedule on a specific set of nodes or a single node currently isn't support. A random node will be selected when running jobs.&#x20;

### Multi-Node Caching

Caching performed using `$Cache` or `Set-PSUCache` is currently limited to the single node that is performing these operations as they are stored in memory on the system. We recommend an external cache, such as Redis, if you wish to cache data across nodes.&#x20;

### Multi-Node Dashboard Broadcast

Multi-Node dashboard broadcast messages are currently not supported. Using cmdlets like `Show-UDToast -Broadcast` will cause a toast to be shown on all connected users to the current node but will not broadcast to the dashboards across all nodes.&#x20;

